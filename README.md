TEST
--------------------------------------------------------------------------------------------------------------------------------------------
The bluetooth devices have services and characteristics, a service can have one or more characteristics.
The data you need to read is stored in some characteristic, all you need to do is find the right characteristic to read.
First print the peripheral once you connect to it.
ble.connect(deviceMac,function(peripheral){
  console.log(peripheral);   //print your peripheral
},function(){
  console.log("error connecting");
})
In the console.you can find the services and characteristic. After finding the right one, start notifications on that characteristic. The code for it:

var service="ffe0"; //or appropriate uuid
var characteristic="ffe1" //or appropriate uuid
ble.startNotification(deviceMac,service,characteristic,function(data){
   try{
       console.log(bytesToString(data)); //convert the array buffer into readable string
   }catch(e){
       console.log(e);
   }
},
function(){
   console.log("error starting notifications.");
});

function bytesToString(buffer) 
{    
    var arr = new Uint8Array(buffer);
    var str = String.fromCharCode.apply(String, arr);
    if(/[\u0080-\uffff]/.test(str))
    {
        throw new Error("this string seems to contain (still encoded) multibytes");
    }
    return str;
}
I think the connection to the peripheral is getting lost somewhere, make sure you stay connected to the peripheral before exchanging data. If you like share the code with me.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
https://stackoverflow.com/questions/40566377/writing-application-code-for-a-ble-scale-all-the-info-included
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
https://stackoverflow.com/questions/63761622/get-weight-data-from-bluetooth-le-scale-by-disassemble-manucaftures-library
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
