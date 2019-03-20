![Logo](api/hilink.png)

Client for Huawei modems with HiLink firmware

Proven on modems:
E3372h-153_Update_22.323.01.00.143_M_AT_05.10
E3372s Update_22.286.53.01.161_S_ADB_TLN_03
   
Firmware and other information can be found here - http://w3bsit3-dns.com.ru/forum/index.php?showtopic=582284&
   

* Installation
   
$ npm install hilinkhuawei   
   
[![NPM version](http://img.shields.io/npm/v/hilinkhuawei.svg)](https://www.npmjs.com/package/hilinkhuawei)    
[![Downloads](https://img.shields.io/npm/dm/hilinkhuawei.svg)](https://www.npmjs.com/package/hilinkhuawei)    
    
Github: https://github.com/bondrogeen/hilinkhuawei    

* Compatibility
E3372 (MTS 827F / 829F, MegaFon M150-2, Beeline E3372 / E3370, TELE2 E3372p-153


	  
* Include  

	var hilink = require('hilinkhuawei');   
	
* Change IP Address (default 192.168.8.1)

	hilink.setIp('192.168.8.x')   
	
* Change the display of traffic statistics (default - 'auto')
    
    'auto' - automatic display in B, KB, MB, GB, TB and time at 00:00:10
    'def' - default traffic in bits, time in seconds.
      
    hilink.setTrafficInfo('def')   
    
* Change modem version (default - '3372s')

    Different versions of hilink firmware have different authentication:
    '3372s' - by token
    '3372h' - by token and cookie
    
    hilink.setModel('3372s')   

* Sending ussd (*100#, callback)
   
    hilink.ussd( '*100#', function( response ){  
        console.log(JSON.stringify(response) );  
    });   

* Answer: *

	{"response":{   
    "content": ["Balance: 88,19r, Limit: 0,01r"],
	"response":"OK"	}   
	}   

 
* Sending SMS (number, text, callback)
  
	hilink.send( '12345678', 'Hello world', function( response ){   
		console.log( JSON.stringify( response, null, 2 ) );  
	});   
	
* Answer: *
  
	{ response: 'OK' }  
	
* Send without saving SMS (number, text, callback)

	hilink.sendAndDelete( '12345678', 'Hello world', function( sendResponse, deleteResponse ){  
		console.log( JSON.stringify(sendResponse) );  
		console.log( JSON.stringify(deleteResponse) );  
	});
	
* Answer: *

	{ response: 'OK' }  
	{ response: 'OK' }  

* Connect to the network ('connect', callback)
* Disconnect from the network ('disconnect', callback)
* Modem reboot ('reboot', callback)

    console.log( JSON.stringify( response, null, 2 ) );   
hilink.control ('connect', function (response) {
});

* Answer: *

{  response: 'OK'  }  


* List of outgoing messages (callback)

	hilink.listOutbox(function( response ){   
 		console.log( JSON.stringify( response, null, 2 ) );  
	});  
	
* Answer: *

   {  
     "response": [   
       {  
         "Smstat": "3",   
         "Index": "40007",   
         "Phone": "123456789",  
         "Content": "4454545454",  
         "Date": "2017-02-25 20:36:30",  
         "Sca": "",   
         "SaveType": "3",  
         "Priority": "4",  
         "SmsType": "1"  
       },  
       {  
         "Smstat": "3",   
         "Index": "40003",  
         "Phone": "123456789",   
         "Content": "121213",  
         "Date": "2017-02-23 14:21:29",   
         "Sca": "",  
         "SaveType": "3",  
         "Priority": "4",  
         "SmsType": "1"  
       }   
     ],  
     "Count": "2"   
   }

    
* List of incoming messages (callback)
  
	hilink.listInbox(function( response ){   
 		console.log( JSON.stringify( response, null, 2 ) );   
	});   
	 
* Answer: *

{  
  "response": [  
    {  
      "Smstat": "0",   
      "Index": "40012",  
      "Phone": "+123456789",  
      "Content": "test",   
      "Date": "2017-02-25 21:04:45",  
      "Sca": "",  
      "SaveType": "4",  
      "Priority": "0",  
      "SmsType": "1"   
    },  
    {   
      "Smstat": "1",  
      "Index": "40001",   
      "Phone": "Balance",   
      "Content": "Баланс:62,39р,Лимит:0,01р",  
      "Date": "2017-02-23 14:20:52",   
      "Sca": "",  
      "SaveType": "4",   
      "Priority": "0",   
      "SmsType": "2" 
    }  
  ],  
  "Count": "2"  
}  
    
 
    
List of new incoming messages only (callback)
    
    hilink.listNew(function(response ){   
        console.log( JSON.stringify( response, null, 2 ) );  
    });   


* Answer: *
    
{  
  "response": [  
    {  
      "Smstat": "0",   
      "Index": "40010",   
      "Phone": "+123456789",   
      "Content": "test text",    
      "Date": "2017-02-25 20:37:53",  
      "Sca": "",    
      "SaveType": "4",  
      "Priority": "0",  
      "SmsType": "1"  
    },  
    {  
      "Smstat": "0",   
      "Index": "40009",   
      "Phone": "+123456789",   
      "Content": "test text",  
      "Date": "2017-02-25 20:37:50",  
      "Sca": "",  
      "SaveType": "4",  
      "Priority": "0",  
      "SmsType": "1"  
    },  
    {  
      "Smstat": "0",  
      "Index": "40008",  
      "Phone": "+123456789",  
      "Content": "test new sms",  
      "Date": "2017-02-25 20:37:47",   
      "Sca": "",   
      "SaveType": "4",   
      "Priority": "0", 
      "SmsType": "1"   
    }
  ],
  "Count": 3
}
    
* Mark as read message (index, callback)
    
    hilink.setRead('40001',function(response ){  
        console.log( JSON.stringify( response, null, 2 ) );  
    });  
    
* Answer: *
 
 {  response: 'OK'  }  
 
* Mark all posts as read

    hilink.readAll(function(response ){  
        console.log( JSON.stringify( response, null, 2 ) );  
    });
 
* Answer: *
  
{  
  "response": [  
    "40022",   
    "40006",  
    "40004"   
  ], 
  "Count": 3   
}   
   
    
* Clearing incoming messages

	hilink.clearInbox();  
	  
* Cleaning outgoing messages

	hilink.clearOutbox();    
  
* Delete message by index

    hilink.delete( '40007', function( response ){    
        console.log(JSON.stringify(response) );    
    });   

* Answer: *

{  response: 'OK'  }   
  

* Status (callback)
  
	hilink.status(function( response ){   
        console.log( JSON.stringify( response, null, 2 ) );   
    });       
   
* Answer: *
     
	{   
      "response": {   
        "ConnectionStatus": "CONNECTED",   
        "SignalIcon": "3",   
        "CurrentNetworkType": "LTE",    
        "CurrentServiceDomain": "3",   
        "RoamingStatus": "0",    
        "simlockStatus": "0",    
        "WanIPAddress": "123.123.123.123",   
        "PrimaryDns": "11.11.24.4",   
        "SecondaryDns": "11.11.114.15",      
        "currenttotalwifiuser": "0",  
        "ServiceStatus": "2",   
        "SimStatus": "1",   
        "CurrentNetworkTypeEx": "101",   
        "maxsignal": "5",    
        "wifiindooronly": "-1",  
        "wififrequence": "0",    
        "classify": "hilink",    
        "flymode": "0"    
      }    
    }     



* Notification (callback)
    
    	hilink.notifications(function( response ){   
            console.log( JSON.stringify( response, null, 2 ) );    
        });      
    
* Answer: *
   
{     
  "response": {     
    "UnreadMessage": "0",    
    "SmsStorageFull": "0",   
    "OnlineUpdateStatus": "10"    
  }     
}    

* Network operator status (callback)

    	hilink.statusNet(function( response ){    
            console.log( JSON.stringify( response, null, 2 ) );   
        });   

* Answer: *

{   
  "response": {   
    "State": "0",    
    "FullName": "MTS-RUS",   
    "ShortName": "MTS",    
    "Numeric": "25001",   
    "Rat": "7"   
  }   
}   

* Condition about count. SMS (callback)

    	hilink.smsCount(function( response ){   
            console.log( JSON.stringify( response, null, 2 ) );   
        });   

* Answer: *
   
{   
  "response": {    
    "LocalUnread": "0",   
    "LocalInbox": "3",    
    "LocalOutbox": "1",   
    "LocalDraft": "2",   
    "LocalDeleted": "0",   
    "SimUnread": "0",      
    "SimInbox": "1",   
    "SimOutbox": "0",   
    "SimDraft": "0",   
    "LocalMax": "500",   
    "SimMax": "5",   
    "SimUsed": "1",    
    "NewMsg": "0"   
  }   
}   
   
* Signal level (callback)
  
    	hilink.signal(function( response ){   
            console.log( JSON.stringify( response, null, 2 ) );   
        });   

* Answer: *

{   
  "response": {    
    "pci": "123",   
    "cell_id": "123456789",   
    "rsrq": "-7dB",    
    "rsrp": "-97dBm",   
    "rssi": "-81dBm",   
    "sinr": "8dB",   
    "mode": "7"   
  }   
}   
   
* Addresses (callback)

    	hilink.settingsNet(function( response ){    
            console.log( JSON.stringify( response, null, 2 ) );    
        });   

* Answer: *

{  
  "response": {   
    "DhcpIPAddress": "192.168.8.1",   
    "DhcpLanNetmask": "255.255.255.0",   
    "DhcpStatus": "1",    
    "DhcpStartIPAddress": "192.168.8.100",   
    "DhcpEndIPAddress": "192.168.8.200",   
    "DhcpLeaseTime": "86400",   
    "DnsStatus": "1",   
    "PrimaryDns": "192.168.8.1",   
    "SecondaryDns": "192.168.8.1"    
  }   
}   

* Information about the modem (callback)

    	hilink.basicInfo(function( response ){
            console.log( JSON.stringify( response, null, 2 ) );
        });

* Answer: *

{   
  "response": {    
    "productfamily": "LTE",    
    "classify": "hilink",   
    "multimode": "0"   
  }   
}   

* Traffic statistics (callback)

    	hilink.traffic(function( response ){
            console.log( JSON.stringify( response, null, 2 ) );
        });

* Answer: *

{
  "response": {
    "CurrentConnectTime": "00:25:46",   
    "CurrentUpload": "1.41 MB",   
    "CurrentDownload": "75.87 MB",   
    "CurrentDownloadRate": "5.35 KB",   
    "CurrentUploadRate": "717 B",   
    "TotalUpload": "455.63 MB",   
    "TotalDownload": "14.66 GB",   
    "TotalConnectTime": "94:34:16",   
    "showtraffic": "1"   
  }
}

* Traffic statistics for the month (callback)


    	hilink.trafficMonth (function( response ) {
            console.log( JSON.stringify( response) );
        });


* Answer: *

{
  "response": {
    "CurrentMonthDownload": "14.67 GB",   
    "CurrentMonthUpload": "455.74 MB",   
    "MonthDuration": "94:35:40",   
    "MonthLastClearTime": "2017-2-21"   
  }
}


   Changelog 
      
   2.1.3   
   
fix ussd  
     
   2.1.1   
   
Added 3372H
   
   2.0.0    
   
Changed the answer
   
   1.1.1    
   
Added new features
   
   1.0.0    
   
Package Request Changes
   
   0.2.1    
   
Added traffic statistics for the month, changed the display of traffic statistics, connection status and network type display.
Added response from the operator from the USSD request.
Delete by post index.
			
			
   0.1.2 
   
   Added ussd commands
   
   0.1.1 

    
