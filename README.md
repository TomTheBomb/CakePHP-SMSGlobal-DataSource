# CakePHP 2.x SMS Global Datasource

A datasource allowing interaction between the SMS Global API.

## INSTALLATION
Copy SmsGlobalSource.php into the app/Model/Datasource directory.

## CONFIGURATION

Within `database.php` add:
```
	public $smsGlobal = array(
		'datasource' => 'SmsGlobalSource',
		'user' => 'USERNAME',
		'password' => 'PASSWORD',
	);
```
Within your `Model` add:
```
	public $useDbConfig = 'smsGlobal';
	public $useTable = false;
```
## USAGE
Making a specific call to an function within the Sms Global wsdl can be done by:

```
$this->Model->apiGetInterface(array('ticket' => $this->Model->getTicketId()));
```

## Explained
```
$this->Model->{APINAME}({REQUIRED PARAMS});
```
For ease of use two functions are available which hold depreciated/default params.

```
$this->Model->checkBalance();
$this->Model->checkBalance('US'); //The param here is the ISO to check your credit against, defaults to AU
```

```
$data = array(
	'sms_from' => 'Fred',
	'sms_to' => '614xxxxxxxx', //International format, without the '+'
	'msg_content' => 'Hello World',
);
$this->Model->sendSms($data);
```

If a response is `FALSE` make a call to `$this->Model->getError();` an error may exist.

## NOTE
Refer to the documentation and wsdl as to what parameters are required per call.
+ http://www.smsglobal.com/docs/SOAP.pdf
+ http://www.smsglobal.com/mobileworks/soapserver.php?wsdl

Ordering matters! If key's are out of order error codes will be thrown from SMS Global.
