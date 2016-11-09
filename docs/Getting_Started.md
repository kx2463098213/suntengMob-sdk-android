# SuntengMob SDK V2.0.3
### 1������sdk
    ��sdk��ѹ���libsĿ¼�µ�jar�ļ����뵽����ָ����libsĿ¼
### 2������AndroidManifest.xml�ļ�
    <!-- �뽫����Ȩ�����ô��븴�Ƶ�AndroidManifest.xml�ļ��У�-->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    
    <!-- ����������Activity��-->
    <activity android:name="com.suntengmob.sdk.activity.InterstitialActivity"
              android:theme="@android:style/Theme.Translucent"
              android:configChanges="orientation|keyboardHidden|screenSize|screenLayout|smallestScreenSize" />
    <activity android:name="com.suntengmob.sdk.activity.BrowserAdActivity"
              android:configChanges="orientation|keyboardHidden|screenSize|screenLayout|smallestScreenSize" />
    <activity android:name="com.suntengmob.sdk.activity.SplashActivity"
              android:screenOrientation="portrait"
              android:resizeableActivity="false"
              android:configChanges="orientation|keyboardHidden|screenSize|screenLayout|smallestScreenSize"/>
    <!-- ����������Activity��-->

#### 3��SDK��ʼ�� 

- **���ó�ʼ��**��
            ����Activity��onCreate()�������澲̬����
             AdService.init(Activity activity, String publisherId, String appKey , String appId);
             
             
 >**ע��:**
 > ����publisherIdΪ�ͻ�ID��appKey��AppId�����sunteng��ȡ

### 4���������չʾ
    /**
     * ��ʾ�������
     */
    private void showInterstitalAd(){
        Ad interstitialAd = new InterstitialAd(); //ʵ����һ���������
        interstitialAd.setPlacementId(51);
        interstitialAd.loadAd( new AdEventListener() {
                    @Override
                    public void onReceiveAd(Ad ad) {
                    //������ɹ���ص�onReceiveAd(),�ڴ�ʱ��ɵ���showAd()���й��չʾ
                        ad.showAd(new AdDisplayListener() {
                            @Override
                            public void onAdDisplayed(Ad ad) {
                                //�������չ��
                            }
                            @Override
                            public void onAdClicked(Ad ad) {
                                //���û�������
                            }
                            @Override
                            public void onAdClosed(Ad ad) {
                               //���û�����رչ����ڹ����水��back��
                            }
                        });
                    }
                    
                    @Override
                    public void onFailedToReceiveAd(Ad ad , int code) {
                        //��������ʧ��ʱ��ص�onFailedToReceiveAd();
                        //���й�澺��ʧ�ܺ�����ɵķ�����������Ҳ��ص�onFailedToReceiveAd();
                        switch (code){
                            case AdService.CODE_BACK_AMOUNT:
                                //������澺��ʧ�ܣ����Ϊ�������޹�淵�أ�
                                break;
                            case AdService.CODE_BLANK_RESPONSE:
                                //��������ʧ�ܣ����Ϊ���ף��޹�淵�أ�
                                break;
                            default:
                                //����ԭ���²���չʾʧ��
                                break;
                        }
                    }
        });
    }
  > **ע��: **
 > ����Ҫ���ù��λid 

### 5���������չʾ

    /**
     * ��ʾ�������
     */
    private void showSplashAd(){
        final int placementid = 49; //���λid
        SplashManager.getIns().loadAd(placementid, new AdEventListener() {
            @Override
            public void onReceiveAd(Ad ad) {
                ad.showAd(new AdDisplayListener() {
                    @Override
                    public void onAdDisplayed(Ad ad) {
                        //�������ɹ���ʾ���ص�
                    }

                    @Override
                    public void onAdClicked(Ad ad) {
                        //������������
                    }

                    @Override
                    public void onAdClosed(Ad ad) {
                        //���������ر�ʱ��ص�
                    }
                });
            }

            @Override
            public void onFailedToReceiveAd(Ad ad, int code) {
                //�����������ʾʧ��ʱ��ص�
                switch (code){
                    case AdService.CODE_BACK_AMOUNT:
                        //��������ʧ�ܣ����Ϊ����
                        break;
                    case AdService.CODE_BLANK_RESPONSE:
                        //��������ʧ�ܣ����Ϊ����
                        break;
                    default:
                       //����ԭ���¿���չʾʧ��
                        break;
                }
            }
        });
    }
  > **ע��: **
 > ����Ҫ���ù��λid
 
### 6��չʾBanner���

       /**
     * ���һ��banner���
     */
    private void showBanner(){
        FrameLayout.LayoutParams layoutParams =
                new FrameLayout.LayoutParams(FrameLayout.LayoutParams.WRAP_CONTENT, FrameLayout.LayoutParams.WRAP_CONTENT);
        layoutParams.gravity = Gravity.BOTTOM | Gravity.RIGHT;

       final int placementId = 50; //���λ��id
        BannerAdView bannerAdView = new BannerAdView(this, placementId ,bannerWidth, bannerHeight); //Ĭ������Ӧ��Ļ
        bannerAdView.setAdListener(new BannerAdListener() {
            @Override
            public void onSwitched(BannerAdView adView) {
                //bannerˢ���л��ɹ�
            }

            @Override
            public void onShowSuccess(BannerAdView adView) {
                //banner��ʾ�ɹ�
            }

            @Override
            public void onShowFailed(BannerAdView adView , int code) {
                Util.printInfo("Show Banner onShowFailed,error code:"+code);
                switch (code){
                    case AdService.CODE_BACK_AMOUNT:
                        //��������ʧ�ܣ�banner����
                        break;
                    case AdService.CODE_BLANK_RESPONSE:
                        //��������ʧ�ܣ�banner����
                        break;
                    default:
                        //����ԭ����bannerչʾʧ��
                        break;
                }
            }
        });
        //��banner�����ӵ�����
        addContentView(bannerAdView, layoutParams);
    }
  > **ע��: **
 > ����Ҫ���ù��λid��  
 
###7�����չʾʧ��ʱ��һЩ������
    AdService.CODE_UNKNOWN_ERROR = -1;//�첽��������з�������
    AdService.CODE_HTTP_ERROR = 1; //����http����Ĺ����з�������
    AdService.CODE_BAD_NETWORK = 0;//�������������Ȩ��
    AdService.CODE_BLANK_RESPONSE = 201 // ��������ʧ��,��������
    AdService.CODE_BACK_AMOUNT = 202; //��������ʧ��,���ط���

###8������Android7.0���������Ҫ֧�ֿ�ֱ���������Σ�
> ���App��Ҫ֧��Android7.0���ϵ��豸��sdk�ṩ��Android7.0�ര��ģʽ���ļ������������Ե�֧�֡�  

**1��Activity��������**
Manifest��ע��SplashActivityʱ����Ҫ����*android:resizeableActivity="false"*

**2��7.0�ļ�����**
**2.1 ��7.0�����ذ�װapk�ļ��������ʹ��FileProvider��������Ҫ��AndroidManifest.xml�������´��룺**

	<!-- ����provider��������7.0, authorities��{{com.sunteng.suntengmob_sample}}�����滻�ɵ�ǰӦ�ð�����
         authorities = "{{BuildConfig.APPLICATION_ID}}.download.download.MobSdk.fileProvider" ,
          provider_pathsΪ������xml�ļ����ڵ���Դ�ļ� -->
	<provider
        android:name="android.support.v4.content.FileProvider"
        android:authorities="com.sunteng.suntengmob_sample.download.MobSdk.fileProvider"
        android:exported="false"
        android:grantUriPermissions="true">
        <meta-data
            android:name="android.support.FILE_PROVIDER_PATHS"
            android:resource="@xml/provider_paths"/>
        </provider>

**2.2.���Կ�����meta-data�У�������һ����Դ·�����ڶ������Ǵ���res/xml/provider_paths.xml�ļ���**
> **ע�⣺ֻ���path��{{com.suntengmob.sdk}}�����滻���㵱ǰ��Ŀ�İ��������Ƶ��ļ��м��ɡ�**

	<?xml version="1.0" encoding="utf-8"?>
	<paths xmlns:android="http://schemas.android.com/apk/res/android">
	     <!--/storage/emulated/0/Android/com.suntengmob.sdk/files/SSP/-->
   		 <!--��path��{{com.sunteng.suntengmob_sample}}�����滻����Ŀ�İ���!-->
  	  	 <external-path name="sunteng_sdk_download_apk" path="Android/data/com.sunteng.suntengmob_sample/files/SSP/"/>
	</paths>
	
###8������
**debugģʽ**
    AdService.setIsDebugModel(boolean debug);
>�������Ϊtrueʱ��Ϊdebugģʽ������־�����Ĭ��ֵΪtrue��������ʽ�汾ʱ����ر�debugģʽ��

**λ����Ϣ��ȡ����**  
    AdService.setLocationEnable(boolean enable);
>�������Ϊtrueʱ����ȡ�û���ǰ����λ�ã�Ĭ��ֵΪtrue�����鿪����
