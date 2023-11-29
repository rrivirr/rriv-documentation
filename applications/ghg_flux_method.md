# GHG Bucket Flux Protocol

## calibration

Constructed a chamber (inverted bucket) with input and output tubes to connect to the LGR-ICOS gas analyzier. 

used expoxy to seal the cables. 

Deployed sensors continuously using the "continoutsPower" branch

RRIV board json format example. replace deploymentIdentifer with descriptoin of run
set-config {"loggerName":"CAL5","siteName":"PDock5","deploymentIdentifier":"PWAdock-cal1.5","wakeInterval":1,"startUpDelay":0,"burstNumber":60,"interBurstDelay":1}
 
AHT json format 
set-slot-config {"slot":1,"type":"adafruit_ahtx0","tag":"aht","burst_size":10}
	-slot 1 is intentioal, maybe should be ahead of ch4 slot
	 
CH4 json format 
set-slot-config {"slot":2,"type":"generic_analog","adc_select":"external","tag":"ch4","burst_size":10}
