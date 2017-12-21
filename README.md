# aliyun-dysms-php-sdk
> 安装方法
```
composer install suhaoxiang/aliyun-dysms-php-sdk
```
>
> 使用方法
```
	use Aliyun\Core\Config as AliyunConfig;
	use Aliyun\Core\Profile\DefaultProfile;
	use Aliyun\Core\DefaultAcsClient;
	use Aliyun\Api\Sms\Request\V20170525\SendSmsRequest;
	use Aliyun\Api\Sms\Request\V20170525\QuerySendDetailsRequest;

	$mobile='xxxxxx';	//电话号码

	$appKey = '';		//app key
	$appSecret = '';	//app secret
	$signName  = '';	//前面
	$template_code = '';//模板名称
	$json_string_param = json_encode(Array(
	    "code"=>rand(100000,999999)
	));

	AliyunConfig::load();
	$profile = DefaultProfile::getProfile("cn-hangzhou", $appKey, $appSecret);
	DefaultProfile::addEndpoint("cn-hangzhou", "cn-hangzhou", "Dysmsapi", "dysmsapi.aliyuncs.com");
	$acsClient = new DefaultAcsClient($profile);
	$request = new SendSmsRequest();
	$request->setPhoneNumbers($mobile);
	$request->setSignName($signName);
	$request->setTemplateCode($template_code);
	if(!empty($json_string_param)) {
	    $request->setTemplateParam($json_string_param);
	}

	$acsResponse =  $acsClient->getAcsResponse($request);

	if($acsResponse && strtolower($acsResponse->Code) == 'ok')
	{
	    return ['code'=>1,"msg"=>"发送短信验证码成功"];
	}
	return ['code'=>0,"msg"=>"发送短信验证码失败"];
```