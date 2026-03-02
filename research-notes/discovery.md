# Discovery Phase

## 1. Basic exploration

```bash
$ adb devices

List of devices attached
M500PSCBYF042200086	device
```

```bash
$ adb shell getprop ro.build.description

sl8541e_1h10wifi5g_32b_Natv-user 10 QP1A.190711.020 49135 release-keys
```

```bash
$ adb shell getprop ro.product.board

sl8541e_1h10wifi5g_32b
```

```bash
$ adb shell uname -a

Linux localhost 4.14.133 #4 SMP PREEMPT Thu Nov 6 18:17:58 CST 2025 armv7l
```

```bash
$ adb shell dmesg | grep -E 'i2c|spi|sensor|imu|gps|camera|accel|gyro|ublox|ov|gc'

[ 7065.712068] type=1400 audit(1772423444.966:5873): avc: denied { dac_override } for comm=75736220666673206F70656E capability=1 scontext=u:r:su:s0 tcontext=u:r:su:s0 tclass=capability permissive=1
[ 7065.712266] type=1400 audit(1772423444.966:5873): avc: denied { dac_override } for comm=75736220666673206F70656E capability=1 scontext=u:r:su:s0 tcontext=u:r:su:s0 tclass=capability permissive=1
[ 7328.235661] type=1400 audit(1772423707.486:5885): avc: denied { dac_override } for comm="sh" capability=1 scontext=u:r:su:s0 tcontext=u:r:su:s0 tclass=capability permissive=1
[ 7328.235850] type=1400 audit(1772423707.486:5885): avc: denied { dac_override } for comm="sh" capability=1 scontext=u:r:su:s0 tcontext=u:r:su:s0 tclass=capability permissive=1
```

## 2. All sensors already exposed by Android?

```bash
$ adb shell dumpsys sensorservice

Captured at: 11:58:19.910
Sensor Device:
Total 8 h/w sensors, 8 running:
0x00000000) active-count = 2; sampling_period(ms) = {20.0, 50.0}, selected = 20.00 ms; batching_period(ms) = {0.0, 0.0}, selected = 0.00 ms
0x00000004) active-count = 2; sampling_period(ms) = {200.0, 20.0}, selected = 20.00 ms; batching_period(ms) = {0.0, 0.0}, selected = 0.00 ms
Sensor List:
0000000000) LSM6DS3TR-C 3-axis Accelerometer | ST              | ver: 1 | type: android.sensor.accelerometer(1) | perm: n/a | flags: 0x00000000
	continuous | minRate=5.00Hz | maxRate=200.00Hz | no batching | non-wakeUp | 
0x00000001) AKM099XX Magnetic field sensor | akm099xx        | ver: 1 | type: android.sensor.magnetic_field(2) | perm: n/a | flags: 0x00000000
	continuous | minRate=5.00Hz | maxRate=50.00Hz | no batching | non-wakeUp | 
0x00000002) MEMSIC Orientation sensor | akm099xx        | ver: 1 | type: android.sensor.orientation(3) | perm: n/a | flags: 0x00000000
	continuous | minRate=5.00Hz | maxRate=50.00Hz | no batching | non-wakeUp | 
0x00000003) LTR558ALS Light sensor    | LTR             | ver: 1 | type: android.sensor.light(5) | perm: n/a | flags: 0x00000002
	on-change | maxDelay=0us | minDelay=0us | no batching | non-wakeUp | 
0x00000004) LTR558ALS Proximity sensor | LTR             | ver: 1 | type: android.sensor.proximity(8) | perm: n/a | flags: 0x00000003
	on-change | maxDelay=0us | minDelay=0us | no batching | wakeUp | 
0x00000005) NULL Sensor               | Null            | ver: 0 | type: android.sensor.gyroscope(4) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | minDelay=0us | no batching | non-wakeUp | 
0x00000006) AKM099XX Rotation vector sensor | akm099xx        | ver: 1 | type: android.sensor.rotation_vector(11) | perm: n/a | flags: 0x00000000
	continuous | minRate=5.00Hz | maxRate=50.00Hz | no batching | non-wakeUp | 
0x00000007) QMP6988 Pressure          | QST             | ver: 1 | type: android.sensor.pressure(6) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=50000.00Hz | FIFO (max,reserved) = (64, 0) events | non-wakeUp | 
0x5f636779) Corrected Gyroscope Sensor | AOSP            | ver: 1 | type: android.sensor.gyroscope(4) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | minDelay=0us | no batching | non-wakeUp | 
0x5f676172) Game Rotation Vector Sensor | AOSP            | ver: 3 | type: android.sensor.game_rotation_vector(15) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
0x5f676273) Gyroscope Bias (debug)    | AOSP            | ver: 1 | type: android.sensor.accelerometer(1) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
0x5f67656f) GeoMag Rotation Vector Sensor | AOSP            | ver: 3 | type: android.sensor.geomagnetic_rotation_vector(20) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
0x5f677276) Gravity Sensor            | AOSP            | ver: 3 | type: android.sensor.gravity(9) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
0x5f6c696e) Linear Acceleration Sensor | AOSP            | ver: 3 | type: android.sensor.linear_acceleration(10) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
0x5f726f76) Rotation Vector Sensor    | AOSP            | ver: 3 | type: android.sensor.rotation_vector(11) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
0x5f797072) Orientation Sensor        | AOSP            | ver: 1 | type: android.sensor.orientation(3) | perm: n/a | flags: 0x00000000
	continuous | maxDelay=0us | maxRate=200.00Hz | no batching | non-wakeUp | 
Fusion States:
9-axis fusion disabled (0 clients), gyro-rate= 200.00Hz, q=< 0, 0, 0, 0 > (0), b=< 0, 0, 0 >
game fusion(no mag) enabled (1 clients), gyro-rate= 200.00Hz, q=< 0, 0, 0, 0 > (0), b=< 0, 0, 0 >
geomag fusion (no gyro) disabled (0 clients), gyro-rate= 200.00Hz, q=< 0, 0, 0, 0 > (0), b=< 0, 0, 0 >
Recent Sensor events:
LTR558ALS Proximity sensor: last 24 events
	 1 (ts=23.156865000, wall=15:29:59.721) 5.00, 0.00, 0.00, 
	 2 (ts=39.232733000, wall=15:30:15.797) 0.00, 0.00, 0.00, 
	 3 (ts=197.186148000, wall=15:32:53.750) 5.00, 0.00, 0.00, 
	 4 (ts=217.948744000, wall=15:33:14.513) 0.00, 0.00, 0.00, 
	 5 (ts=1026.407106000, wall=10:10:05.670) 5.00, 0.00, 0.00, 
	 6 (ts=1042.886550000, wall=10:10:22.150) 0.00, 0.00, 0.00, 
	 7 (ts=1049.532818000, wall=10:10:28.796) 5.00, 0.00, 0.00, 
	 8 (ts=1054.628115000, wall=10:10:33.891) 0.00, 0.00, 0.00, 
	 9 (ts=1067.166009000, wall=10:10:46.429) 5.00, 0.00, 0.00, 
	10 (ts=1071.080224000, wall=10:10:50.343) 0.00, 0.00, 0.00, 
	11 (ts=1083.992542000, wall=10:11:03.256) 5.00, 0.00, 0.00, 
	12 (ts=1148.609624000, wall=10:12:07.873) 0.00, 0.00, 0.00, 
	13 (ts=1154.082711000, wall=10:12:13.346) 5.00, 0.00, 0.00, 
	14 (ts=1157.212733000, wall=10:12:16.476) 0.00, 0.00, 0.00, 
	15 (ts=1164.659084000, wall=10:12:23.922) 5.00, 0.00, 0.00, 
	16 (ts=1172.098593000, wall=10:12:31.362) 0.00, 0.00, 0.00, 
	17 (ts=1677.819677000, wall=10:20:57.083) 5.00, 0.00, 0.00, 
	18 (ts=1678.993778000, wall=10:20:58.257) 0.00, 0.00, 0.00, 
	19 (ts=1679.777793000, wall=10:20:59.041) 5.00, 0.00, 0.00, 
	20 (ts=1680.168914000, wall=10:20:59.432) 0.00, 0.00, 0.00, 
	21 (ts=5480.980368000, wall=11:24:20.244) 5.00, 0.00, 0.00, 
	22 (ts=5492.700035000, wall=11:24:31.963) 0.00, 0.00, 0.00, 
	23 (ts=5494.654051000, wall=11:24:33.917) 5.00, 0.00, 0.00, 
	24 (ts=5524.315905000, wall=11:25:03.579) 0.00, 0.00, 0.00, 
LSM6DS3TR-C 3-axis Accelerometer: last 50 events
	 1 (ts=7519.655989000, wall=11:58:18.919) 0.03, 6.47, 7.87, 
	 2 (ts=7519.675881000, wall=11:58:18.939) 0.05, 6.47, 7.88, 
	 3 (ts=7519.695956000, wall=11:58:18.959) 0.06, 6.45, 7.88, 
	 4 (ts=7519.716271000, wall=11:58:18.979) 0.04, 6.46, 7.86, 
	 5 (ts=7519.736036000, wall=11:58:18.999) 0.08, 6.47, 7.86, 
	 6 (ts=7519.756067000, wall=11:58:19.019) 0.05, 6.48, 7.85, 
	 7 (ts=7519.776099000, wall=11:58:19.039) 0.02, 6.49, 7.85, 
	 8 (ts=7519.796131000, wall=11:58:19.059) 0.04, 6.49, 7.80, 
	 9 (ts=7519.816150000, wall=11:58:19.079) 0.06, 6.50, 7.83, 
	10 (ts=7519.836181000, wall=11:58:19.099) 0.08, 6.49, 7.81, 
	11 (ts=7519.856149000, wall=11:58:19.119) 0.08, 6.50, 7.85, 
	12 (ts=7519.876136000, wall=11:58:19.139) 0.08, 6.51, 7.85, 
	13 (ts=7519.896186000, wall=11:58:19.159) 0.06, 6.49, 7.85, 
	14 (ts=7519.916264000, wall=11:58:19.179) 0.04, 6.48, 7.83, 
	15 (ts=7519.936341000, wall=11:58:19.199) 0.04, 6.45, 7.83, 
	16 (ts=7519.956230000, wall=11:58:19.219) 0.04, 6.45, 7.85, 
	17 (ts=7519.976514000, wall=11:58:19.239) 0.05, 6.46, 7.89, 
	18 (ts=7519.996454000, wall=11:58:19.259) 0.05, 6.46, 7.89, 
	19 (ts=7520.017047000, wall=11:58:19.280) 0.05, 6.46, 7.87, 
	20 (ts=7520.036884000, wall=11:58:19.300) 0.03, 6.43, 7.84, 
	21 (ts=7520.057008000, wall=11:58:19.320) 0.04, 6.46, 7.85, 
	22 (ts=7520.076918000, wall=11:58:19.340) 0.07, 6.46, 7.86, 
	23 (ts=7520.097039000, wall=11:58:19.360) 0.10, 6.53, 7.96, 
	24 (ts=7520.117109000, wall=11:58:19.380) 0.04, 6.41, 7.82, 
	25 (ts=7520.137133000, wall=11:58:19.400) 0.01, 6.48, 7.75, 
	26 (ts=7520.157165000, wall=11:58:19.420) 0.01, 6.47, 7.78, 
	27 (ts=7520.177408000, wall=11:58:19.440) 0.04, 6.49, 7.72, 
	28 (ts=7520.197437000, wall=11:58:19.460) 0.08, 6.53, 7.86, 
	29 (ts=7520.217469000, wall=11:58:19.480) 0.23, 6.43, 7.90, 
	30 (ts=7520.237617000, wall=11:58:19.500) 0.20, 6.44, 8.07, 
	31 (ts=7520.257918000, wall=11:58:19.521) 0.14, 6.43, 8.01, 
	32 (ts=7520.277747000, wall=11:58:19.540) -0.05, 6.45, 7.69, 
	33 (ts=7520.297625000, wall=11:58:19.560) -0.03, 6.44, 7.71, 
	34 (ts=7520.317693000, wall=11:58:19.580) 0.02, 6.40, 7.86, 
	35 (ts=7520.338010000, wall=11:58:19.601) 0.11, 6.43, 7.95, 
	36 (ts=7520.358051000, wall=11:58:19.621) 0.12, 6.42, 7.98, 
	37 (ts=7520.378027000, wall=11:58:19.641) 0.05, 6.46, 7.87, 
	38 (ts=7520.398220000, wall=11:58:19.661) -0.02, 6.51, 7.95, 
	39 (ts=7520.418402000, wall=11:58:19.681) -0.03, 6.36, 7.80, 
	40 (ts=7520.438446000, wall=11:58:19.701) 0.06, 6.50, 7.87, 
	41 (ts=7520.458781000, wall=11:58:19.721) 0.12, 6.47, 7.86, 
	42 (ts=7520.478854000, wall=11:58:19.742) 0.14, 6.55, 7.93, 
	43 (ts=7520.499184000, wall=11:58:19.762) 0.12, 6.52, 7.84, 
	44 (ts=7520.519243000, wall=11:58:19.782) 0.01, 6.51, 7.74, 
	45 (ts=7520.539451000, wall=11:58:19.802) -0.04, 6.50, 7.71, 
	46 (ts=7520.559495000, wall=11:58:19.822) 0.03, 6.48, 7.74, 
	47 (ts=7520.582327000, wall=11:58:19.845) 0.14, 6.49, 7.91, 
	48 (ts=7520.599573000, wall=11:58:19.862) 0.14, 6.52, 7.91, 
	49 (ts=7520.619581000, wall=11:58:19.882) 0.06, 6.51, 7.87, 
	50 (ts=7520.639694000, wall=11:58:19.903) 0.03, 6.44, 7.81, 
Active sensors:
LSM6DS3TR-C 3-axis Accelerometer (handle=0x00000000, connections=1)
LTR558ALS Proximity sensor (handle=0x00000004, connections=2)
Socket Buffer size = 984 events
WakeLock Status: not held 
Mode : NORMAL
Sensor Privacy: disabled
4 active connections
Connection Number: 0 
	Operating Mode: NORMAL
	 i1.t | WakeLockRefCount 0 | uid 1000 | cache size 0 | max cache size 0
	 LTR558ALS Proximity sensor 0x00000004 | status: active | pending flush events 0 
Connection Number: 1 
	Operating Mode: NORMAL
	 com.android.systemui.classifier.brightline.BrightLineFalsingManager | WakeLockRefCount 0 | uid 10091 | cache size 0 | max cache size 0
	 LTR558ALS Proximity sensor 0x00000004 | status: active | pending flush events 0 
Connection Number: 2 
	Operating Mode: NORMAL
	 i1.t | WakeLockRefCount 0 | uid 1000 | cache size 0 | max cache size 0
	 LSM6DS3TR-C 3-axis Accelerometer 0x00000000 | status: active | pending flush events 0 
Connection Number: 3 
	Operating Mode: NORMAL
	 i1.t | WakeLockRefCount 0 | uid 1000 | cache size 0 | max cache size 0
	 Gravity Sensor 0x5f677276 | status: active | pending flush events 0 
0 direct connections
Previous Registrations:
10:39:15 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:38:34 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:14:45 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:14:10 + 0x00000005 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=10000us batchingPeriod=0us
10:14:10 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:13:08 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:11:46 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:11:24 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:10:08 + 0x00000005 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=10000us batchingPeriod=0us
10:10:08 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:09:45 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:08:51 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:05:09 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:05:01 + 0x00000005 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=10000us batchingPeriod=0us
10:05:01 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:04:18 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:04:18 - 0x00000003 pid= 1691 uid= 1000 package=u5.a
10:03:20 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
10:03:17 + 0x00000003 pid= 1691 uid= 1000 package=u5.a samplingPeriod=200000us batchingPeriod=0us
10:03:01 - 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358
10:02:58 + 0x00000005 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=10000us batchingPeriod=0us
10:02:58 + 0x00000000 pid=  781 uid= 1000 package=hidl_client_pid_358 samplingPeriod=50000us batchingPeriod=0us
14:30:04 + 0x5f677276 pid= 1691 uid= 1000 package=i1.t samplingPeriod=200000us batchingPeriod=0us
14:30:04 + 0x00000000 pid= 1691 uid= 1000 package=i1.t samplingPeriod=20000us batchingPeriod=0us
14:30:04 + 0x00000004 pid= 1691 uid= 1000 package=i1.t samplingPeriod=200000us batchingPeriod=0us
14:29:58 + 0x00000004 pid= 1018 uid=10091 package=com.android.systemui.classifier.brightline.BrightLineFalsingManager samplingPeriod=20000us batchingPeriod=0us
```

```bash
$ adb shell dumpsys location

Current Location Manager state:
  Current System Time: 03-02 11:59:18.375, Current Elapsed Time: +2h6m19s112ms
  Current user: 0 [0]
  Location mode: true
  Battery Saver Location Mode: NO_CHANGE
  Location Listeners:
    Reciever[52482e3 listener UpdateRecord[passive com.cloudwinner.cloudvideo(1000 foreground) Request[POWER_NONE passive fastest=+9s0ms] null] monitoring location: true]
    Reciever[d5b7d15 listener UpdateRecord[passive android(1000 foreground) Request[POWER_NONE passive fastest=+30m0s0ms] null] monitoring location: true]
    Reciever[e6b833c listener UpdateRecord[passive android(1000 foreground) Request[POWER_NONE passive fastest=0] null] monitoring location: false]
    Reciever[385399 listener UpdateRecord[gps com.cloudwinner.cloudvideo(1000 foreground) Request[ACCURACY_FINE gps requested=+1s0ms fastest=+1s0ms] null] monitoring location: true]
  Active Records by Provider:
    gps:
      UpdateRecord[gps com.cloudwinner.cloudvideo(1000 foreground) Request[ACCURACY_FINE gps requested=+1s0ms fastest=+1s0ms] null]
    passive:
      UpdateRecord[passive android(1000 foreground) Request[POWER_NONE passive fastest=0] null]
      UpdateRecord[passive android(1000 foreground) Request[POWER_NONE passive fastest=+30m0s0ms] null]
      UpdateRecord[passive com.cloudwinner.cloudvideo(1000 foreground) Request[POWER_NONE passive fastest=+9s0ms] null]
  Active GnssMeasurement Listeners:
  Active GnssNavigationMessage Listeners:
  Active GnssStatus Listeners:
    8454 1000 com.cloudwinner.cloudvideo: true
    8454 1000 com.cloudwinner.cloudvideo: true
    1691 1000 com.cloudwinner.cloudvideo: true
  Historical Records by Provider:
    android: passive: Min interval 0 seconds: Max interval 1800 seconds: Duration requested 126 total, 126 foreground, out of the last 126 minutes: Currently active
    com.cloudwinner.cloudvideo: passive: Interval 9 seconds: Duration requested 116 total, 116 foreground, out of the last 117 minutes: Currently active
    com.cloudwinner.cloudvideo: gps: Interval 1 seconds: Duration requested 116 total, 116 foreground, out of the last 117 minutes: Currently active
  Last Known Locations:
  Last Known Locations Coarse Intervals:
  Geofences:
  mWhitelist=[] mBlacklist=[]
  fudger: offset: 930, -99 (meters)
  passive provider:
    useable=true
    properties=com.android.internal.location.ProviderProperties@a972ab8
 report location=true
  gps provider:
    useable=true
    properties=com.android.internal.location.ProviderProperties@3b17091
  mStarted=true   (changed +32m35s132ms ago)
  mFixInterval=1000
  mLowPowerMode=false
  mGnssMeasurementsProvider.isRegistered()=false
  mGnssNavigationMessageProvider.isRegistered()=false
  mDisableGpsForPowerManager=false
  mTopHalCapabilities=0xd6 ( MSB MSA ON_DEMAND_TIME MEASUREMENTS NAV_MESSAGES )
GNSS_KPI_START
  KPI logging start time: +17s241ms
  KPI logging end time: +2h6m19s114ms
  Number of location reports: 0
  Number of TTFF reports: 0
  Number of position accuracy reports: 0
  Number of CN0 reports: 0
  Used-in-fix constellation types: 
GNSS_KPI_END
Power Metrics
  Time on battery (min): 87.23118333333333
  Amount of time (while on battery) Top 4 Avg CN0 > 20.0 dB-Hz (min): 0.0
  Amount of time (while on battery) Top 4 Avg CN0 <= 20.0 dB-Hz (min): 1.8972833333333334
  Energy consumed while on battery (mAh): 0.5628605555555556
Hardware Version: 
  native internal state: Gnss Location Data:: LatitudeDegrees: 37.422, LongitudeDegrees: -122.084, altitudeMeters: 1.60063, speedMetersPerSecond: 0, bearingDegrees: 0, horizontalAccuracyMeters: 5, verticalAccuracyMeters: 5, speedAccuracyMetersPerSecond: 1, bearingAccuracyDegrees: 90, ageSeconds: 0.99
Gnss Time Data:: timeEstimate: 1519930775453, timeUncertaintyNs: 1000, frequencyUncertaintyNsPerSec: 50000
constell: 1=GPS, 2=SBAS, 3=GLO, 4=QZSS, 5=BDS, 6=GAL, 7=IRNSS; ephType: 0=Eph, 1=Alm, 2=Unk; ephSource: 0=Demod, 1=Supl, 2=Server, 3=Unk; ephHealth: 0=Good, 1=Bad, 2=Unk

  fused provider:
    useable=true
    properties=com.android.internal.location.ProviderProperties@3ff4bf6
    service={com.android.location.fused/com.android.location.fused.FusedLocationService}@0
```

## 3. I2C / SPI buses

```bash
$ adb shell ls -l /dev/i2c*

ls: /dev/i2c-10: No such file or directory
ls: /dev/i2c-11: No such file or directory
ls: /dev/i2c-12: No such file or directory
ls: /dev/i2c-13: No such file or directory
ls: /dev/i2c-14: No such file or directory
ls: /dev/i2c-15: No such file or directory
ls: /dev/i2c-16: No such file or directory
ls: /dev/i2c-17: No such file or directory
ls: /dev/i2c-18: No such file or directory
ls: /dev/i2c-19: No such file or directory
ls: /dev/i2c-20: No such file or directory
ls: /dev/i2c-21: No such file or directory
ls: /dev/i2c-5: No such file or directory
ls: /dev/i2c-6: No such file or directory
ls: /dev/i2c-7: No such file or directory
ls: /dev/i2c-8: No such file or directory
ls: /dev/i2c-9: No such file or directory
crw------- 1 root root 89,   0 2025-12-11 15:29 /dev/i2c-0
crw------- 1 root root 89,   1 2025-12-11 15:29 /dev/i2c-1
crw------- 1 root root 89,   2 2025-12-11 15:29 /dev/i2c-2
crw------- 1 root root 89,   3 2025-12-11 15:29 /dev/i2c-3
crw------- 1 root root 89,   4 2025-12-11 15:29 /dev/i2c-4
```

```bash
$ adb shell ls -l /dev/spidev*

ls: /dev/spidev*: No such file or directory
```

```bash
$ adb shell ls /sys/bus/i2c/devices/

1-0020
1-0060
2-0023
2-0068
2-006b
2-006c
3-0014
3-002e
i2c-0
i2c-1
i2c-2
i2c-3
i2c-4
```

```bash
$ adb shell ls /sys/bus/iio/devices/

iio:device0
```

## 4. Cameras & Video

```bash
$ adb shell ls /dev/video*

ls: /dev/video*: No such file or directory
```

```bash
$ adb shell "dumpsys media.camera | grep -E 'Camera ID|Facing|Device'"

    Device 0 maps to "0"
    Device 1 maps to "1"
  12-11 14:29:45 : ADD device 0, reason: (Device added)
  12-11 14:29:45 : ADD device 1, reason: (Device added)
  Device 0 is closed, no client instance
  Device 1 is closed, no client instance
    Facing: Back
    Facing: Front
    Facing: Front
    Facing: Back
    Facing: Back
    Facing: Front
    Facing: Front
    Facing: Back
    Facing: Back
    Facing: Front
    0x80000033 (sprd3DeviceOrientation) with type 1 (int32) defined in section com.addParameters
```

## 5. GPS serial ports (very common)

```bash
$ adb shell ls /dev/ttyS* /dev/ttyUSB*

ls: /dev/ttyS0: No such file or directory
ls: /dev/ttyS10: No such file or directory
ls: /dev/ttyS11: No such file or directory
ls: /dev/ttyS12: No such file or directory
ls: /dev/ttyS13: No such file or directory
ls: /dev/ttyS14: No such file or directory
ls: /dev/ttyS15: No such file or directory
ls: /dev/ttyS16: No such file or directory
ls: /dev/ttyS17: No such file or directory
ls: /dev/ttyS18: No such file or directory
ls: /dev/ttyS19: No such file or directory
ls: /dev/ttyS2: No such file or directory
ls: /dev/ttyS20: No such file or directory
ls: /dev/ttyS21: No such file or directory
ls: /dev/ttyS22: No such file or directory
ls: /dev/ttyS23: No such file or directory
ls: /dev/ttyS24: No such file or directory
ls: /dev/ttyS25: No such file or directory
ls: /dev/ttyS26: No such file or directory
ls: /dev/ttyS27: No such file or directory
ls: /dev/ttyS28: No such file or directory
ls: /dev/ttyS29: No such file or directory
ls: /dev/ttyS3: No such file or directory
ls: /dev/ttyS30: No such file or directory
ls: /dev/ttyS31: No such file or directory
ls: /dev/ttyS4: No such file or directory
ls: /dev/ttyS5: No such file or directory
ls: /dev/ttyS6: No such file or directory
ls: /dev/ttyS7: No such file or directory
ls: /dev/ttyS8: No such file or directory
ls: /dev/ttyS9: No such file or directory
ls: /dev/ttyUSB*: No such file or directory
/dev/ttyS1
```

## 6. Input events (sometimes IMU appears here)

```bash
$ adb shell getevent -lp | grep -E 'ABS|REL|EV_KEY'

    REL (0002): REL_X                 REL_Y                 REL_Z                 REL_RX               
could not get driver version for /dev/input/mice, Not a typewriter
                REL_RY                REL_MISC             
    REL (0002): REL_X                 REL_Y                 REL_Z                 REL_RX               
                REL_RY                REL_MISC             
    REL (0002): REL_X                 REL_Y                 REL_HWHEEL           
    ABS (0003): ABS_X                 : value 0, min 0, max 1200, fuzz 0, flat 0, resolution 0
                ABS_Y                 : value 0, min -40, max 85, fuzz 0, flat 0, resolution 0
                ABS_THROTTLE          : value 0, min 0, max 3, fuzz 0, flat 0, resolution 0
    ABS (0003): ABS_DISTANCE          : value 0, min 0, max 1, fuzz 0, flat -1, resolution 0
                ABS_MISC              : value 0, min 0, max 100001, fuzz 0, flat -1, resolution 0

```

## 7. Extract Device Tree (this is the "schematic" we can read!)

```bash
adb shell "su -c 'dd if=/sys/firmware/fdt of=/sdcard/helmet-dtb.img'"
adb pull /sdcard/helmet-dtb.img .
dtc -I dtb -O dts -o helmet.dts helmet-dtbs.img
```

[helmet.dts](/research-notes/helmet_key.txt)