# dashboard-api-status

Status of the Android APIs that Dashboard relies upon. Because they will
probably start disappearing one by one in the future (Data already has!).

These are provided either as the API methods, or pseudocode if they're hacky.


## Wifi

Get: `WifiManager.setWifiEnabled()`

Set: `WifiManager.isWifiEnabled()`


## Data

Get: `NetworkInfo.getNetworkInfo(ConnectivityManager.TYPE_MOBILE).getState()`

Set (Android 4.4 and below): 
`ConnectivityManager.class.getDeclaredMethod("setMobileDataEnabled", boolean.class);`

Set (Android 5.0 and above, requires root):
```
"# service call phone" 
  + getTransactionCode("com.android.internal.telephony.ITelephony", "setDataEnabled")
  + " i32 " + (enabled ? "1" : "0")
  + "\n exit"
```