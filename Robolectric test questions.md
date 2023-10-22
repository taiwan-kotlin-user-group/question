## 進行 Robolectric 測試， 使用 Hilt 依賴注入的 Activity 沒有注入資料

### 程式碼

#### Robolectric 測試

```java=

@HiltAndroidTest
@RunWith(RobolectricTestRunner.class)
@Config(application = HiltTestApplication.class)
public class RobolectricTest {

    ActivityController<TestActivity> controller ;
    public HiltAndroidRule hiltRule = new HiltAndroidRule(this);

    @Before
    public void setUp(){
        hiltRule.inject();
        controller = Robolectric.buildActivity(TestActivity.class);
    }

    @Test
    public void  Test1(){
        TestActivity activity = controller.setup().get();
        .....  
    }

}

```

#### 測試 Activity

```kotlin =

@AndroidEntryPoint
class TestActivity : AppCompatActivity() {
    @Inject
    lateinit var appSettingStorage: AppSettingStorage

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_test)
        val isTurnOffNotifications = appSettingStorage.getIsTurnOffNotifications()
        .....   
    }
}


```

### 問題

#### 上面 Robolectric 測試 Test1() 時，運行到 controller.setup() 會出現 UninitializedPropertyAccessException ，原因是 TestActivity 在 OnCreate 調用 appSettingStorage.getIsTurnOffNotifications() ，但 appSettingStorage 沒有被注入資料。


### 解決方式

#### 修改測試的 TestActivity 原本繼承的 class 為 Hilt_TestActivity，規則是  Hilt_+ Activity名稱。並且要在 @AndroidEntryPoint 後面加上一個括號，裡面填寫原本繼承的 class 名稱。


```kotlin =

@AndroidEntryPoint(AppCompatActivity::class)
class TestActivity : Hilt_TestActivity() {
    @Inject
    lateinit var appSettingStorage: AppSettingStorage

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_test)
        val isTurnOffNotifications = appSettingStorage.getIsTurnOffNotifications()
        .....   
    }
}

```