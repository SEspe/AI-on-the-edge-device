[Overview](_OVERVIEW.md) 

## REST API endpoint: config

`http://IP-ADDRESS/config`


Get and set process related configuration parameter. The data is provided / needs to be 
provided in JSON notation.<br> Parameter description for every single parameter is 
located at github repository (`docs/Configuration/Parameter`) or can be displayed on 
WebUI configuration page (question mark symbol next to each parameter). 

- JSON: `/config`
- HTML: `/config?task=reload`

1. Get API name and version:
    - Payload:
      - `/config?task=api_name`
    - Response:
      - Content type: `HTML`
      - Content: HTML query response, e.g. `config:v1`

2. HTML query request to reload configuration and reinit process:
    - Payload:
      - `/config?task=reload`
    - Response:
      - Content type: `HTML`
      - Content: HTML query response

3. Get config in JSON notation (GET handler)
    - Payload:
      - No payload needed
    - Response:
      - Content type: `JSON`
      - Content: JSON response
    - Example: see below

4. Set config in JSON notation (POST handler)
    - Payload:
      - Configuration in JSON notation
      - Setting only a single, some parameter or all parameter is supported
    - Response:
      - POST handler status response
    - Example: see below

```
{
    "config":  {
                   "version":  6,
                   "lastmodified":  "2026-01-01T00:00:00+0100"
               },
    "operationmode":  {
                          "opmode":  1,
                          "automaticprocessinterval":  "2.00",
                          "usedemoimages":  false
                      },
    "takeimage":  {
                      "flashlight":  {
                                         "flashtime":  2000,
                                         "flashintensity":  20
                                     },
                      "camera":  {
                                     "cameramodel":  2,
                                     "camerafrequency":  10,
                                     "imagequality":  12,
                                     "brightness":  0,
                                     "contrast":  0,
                                     "saturation":  0,
                                     "sharpness":  0,
                                     "exposurecontrolmode":  1,
                                     "autoexposurelevel":  0,
                                     "manualexposurevalue":  300,
                                     "gaincontrolmode":  1,
                                     "manualgainvalue":  0,
                                     "specialeffect":  0,
                                     "mirrorimage":  true,
                                     "flipimage":  false,
                                     "zoomfactor":  1344,
                                     "zoomoffsetx":  120,
                                     "zoomoffsety":  76
                                 },
                      "debug":  {
                                    "saverawimages":  false,
                                    "rawimageslocation":  "/log/source",
                                    "rawimagesretention":  3
                                }
                  },
    "imagealignment":  {
                           "alignmentalgo":  0,
                           "searchfield":  {
                                               "x":  20,
                                               "y":  20
                                           },
                           "imagerotation":  "127.8",
                           "marker":  [
                                          {
                                              "x":  30,
                                              "y":  290
                                          },
                                          {
                                              "x":  559,
                                              "y":  103
                                          }
                                      ],
                           "debug":  {
                                         "savedebuginfo":  false
                                     }
                       },
    "numbersequences":  {
                            "sequence":  [
                                             {
                                                 "sequenceid":  0,
                                                 "sequencename":  "main"
                                             }
                                         ]
                        },
    "digit":  {
                  "enabled":  true,
                  "model":  "dig-class11_1701_s2.tflite",
                  "cnngoodthreshold":  "0.80",
                  "sequence":  [
                                   {
                                       "sequenceid":  0,
                                       "sequencename":  "main",
                                       "roi":  [
                                                   {
                                                       "x":  213,
                                                       "y":  151,
                                                       "dx":  54,
                                                       "dy":  89
                                                   },
                                                   {
                                                       "x":  261,
                                                       "y":  142,
                                                       "dx":  68,
                                                       "dy":  111
                                                   },
                                                   {
                                                       "x":  317,
                                                       "y":  158,
                                                       "dx":  46,
                                                       "dy":  81
                                                   },
                                                   {
                                                       "x":  359,
                                                       "y":  148,
                                                       "dx":  56,
                                                       "dy":  88
                                                   },
                                                   {
                                                       "x":  411,
                                                       "y":  149,
                                                       "dx":  53,
                                                       "dy":  89
                                                   },
                                                   {
                                                       "x":  468,
                                                       "y":  142,
                                                       "dx":  48,
                                                       "dy":  101
                                                   }
                                               ]
                                   }
                               ],
                  "debug":  {
                                "saveroiimages":  false,
                                "roiimageslocation":  "/log/digit",
                                "roiimagesretention":  3,
                                "roisavingsize":  0
                            }
              },
    "analog":  {
                   "enabled":  false,
                   "model":  "ana-class100_0201_s1_q.tflite",
                   "sequence":  [
                                    {
                                        "sequenceid":  0,
                                        "sequencename":  "main",
                                        "roi":  [

                                                ]
                                    }
                                ],
                   "debug":  {
                                 "saveroiimages":  false,
                                 "roiimageslocation":  "/log/analog",
                                 "roiimagesretention":  3,
                                 "roisavingsize":  0
                             }
               },
    "postprocessing":  {
                           "sequence":  [
                                            {
                                                "sequenceid":  0,
                                                "sequencename":  "main",
                                                "decimalshift":  -3,
                                                "analogdigitsyncvalue":  "9.2",
                                                "extendedresolution":  true,
                                                "ignoreleadingnan":  false,
                                                "checkdigitincreaseconsistency":  false,
                                                "maxratechecktype":  1,
                                                "maxrate":  "0.150",
                                                "allownegativerate":  false,
                                                "usefallbackvalue":  false,
                                                "fallbackvalueagestartup":  720
                                            }
                                        ],
                           "debug":  {
                                         "savedebuginfo":  false
                                     }
                       },
    "mqtt":  {
                 "enabled":  true,
                 "uri":  "",
                 "maintopic":  "watermeter",
                 "clientid":  "watermeter",
                 "authmode":  1,
                 "username":  "",
                 "password":  "",
                 "tls":  {
                             "servercertverification":  2,
                             "cacert":  "",
                             "clientcert":  "",
                             "clientkey":  ""
                         },
                 "processdatanotation":  0,
                 "retainprocessdata":  false,
                 "homeassistant":  {
                                       "discoveryenabled":  true,
                                       "discoveryprefix":  "homeassistant",
                                       "statustopic":  "homeassistant/status",
                                       "metertype":  1,
                                       "retaindiscovery":  false
                                   }
             },
    "influxdbv1":  {
                       "enabled":  false,
                       "uri":  "",
                       "database":  "",
                       "authmode":  0,
                       "username":  "",
                       "password":  "",
                       "tls":  {
                                   "servercertverification":  2,
                                   "cacert":  "",
                                   "clientcert":  "",
                                   "clientkey":  ""
                               },
                       "sequence":  [
                                        {
                                            "sequenceid":  0,
                                            "sequencename":  "main",
                                            "measurementname":  "",
                                            "fieldkey1":  ""
                                        }
                                    ]
                   },
    "influxdbv2":  {
                       "enabled":  false,
                       "uri":  "",
                       "bucket":  "",
                       "organization":  "",
                       "authmode":  1,
                       "token":  "",
                       "tls":  {
                                   "servercertverification":  2,
                                   "cacert":  "",
                                   "clientcert":  "",
                                   "clientkey":  ""
                               },
                       "sequence":  [
                                        {
                                            "sequenceid":  0,
                                            "sequencename":  "main",
                                            "measurementname":  "",
                                            "fieldkey1":  ""
                                        }
                                    ]
                   },
    "webhook":  {
                    "enabled":  false,
                    "uri":  "",
                    "apikey":  "",
                    "publishimage":  0,
                    "authmode":  0,
                    "username":  "",
                    "password":  "",
                    "tls":  {
                                "servercertverification":  2,
                                "cacert":  "",
                                "clientcert":  "",
                                "clientkey":  ""
                            }
                },
    "gpio":  {
                 "customizationenabled":  false,
                 "gpiopin":  [
                                 {
                                     "gpionumber":  1,
                                     "gpiousage":  "restricted: uart0-tx",
                                     "pinenabled":  false,
                                     "pinname":  "",
                                     "pinmode":  "input",
                                     "capturemode":  "cyclic-polling",
                                     "inputdebouncetime":  200,
                                     "pwmfrequency":  5000,
                                     "logicactivelow":  false,
                                     "exposetomqtt":  false,
                                     "exposetorest":  false,
                                     "smartled":  {
                                                      "type":  0,
                                                      "quantity":  1,
                                                      "colorredchannel":  255,
                                                      "colorgreenchannel":  255,
                                                      "colorbluechannel":  255
                                                  },
                                     "intensitycorrectionfactor":  100
                                 },
                                 {
                                     "gpionumber":  3,
                                     "gpiousage":  "restricted: uart0-rx",
                                     "pinenabled":  false,
                                     "pinname":  "",
                                     "pinmode":  "input",
                                     "capturemode":  "cyclic-polling",
                                     "inputdebouncetime":  200,
                                     "pwmfrequency":  5000,
                                     "logicactivelow":  false,
                                     "exposetomqtt":  false,
                                     "exposetorest":  false,
                                     "smartled":  {
                                                      "type":  0,
                                                      "quantity":  1,
                                                      "colorredchannel":  255,
                                                      "colorgreenchannel":  255,
                                                      "colorbluechannel":  255
                                                  },
                                     "intensitycorrectionfactor":  100
                                 },
                                 {
                                     "gpionumber":  4,
                                     "gpiousage":  "flashlight-pwm",
                                     "pinenabled":  false,
                                     "pinname":  "",
                                     "pinmode":  "flashlight-default",
                                     "capturemode":  "cyclic-polling",
                                     "inputdebouncetime":  200,
                                     "pwmfrequency":  5000,
                                     "logicactivelow":  false,
                                     "exposetomqtt":  false,
                                     "exposetorest":  false,
                                     "smartled":  {
                                                      "type":  0,
                                                      "quantity":  1,
                                                      "colorredchannel":  255,
                                                      "colorgreenchannel":  255,
                                                      "colorbluechannel":  255
                                                  },
                                     "intensitycorrectionfactor":  100
                                 },
                                 {
                                     "gpionumber":  12,
                                     "gpiousage":  "spare",
                                     "pinenabled":  false,
                                     "pinname":  "",
                                     "pinmode":  "input",
                                     "capturemode":  "cyclic-polling",
                                     "inputdebouncetime":  200,
                                     "pwmfrequency":  5000,
                                     "logicactivelow":  false,
                                     "exposetomqtt":  false,
                                     "exposetorest":  false,
                                     "smartled":  {
                                                      "type":  0,
                                                      "quantity":  1,
                                                      "colorredchannel":  255,
                                                      "colorgreenchannel":  255,
                                                      "colorbluechannel":  255
                                                  },
                                     "intensitycorrectionfactor":  100
                                 },
                                 {
                                     "gpionumber":  13,
                                     "gpiousage":  "spare",
                                     "pinenabled":  false,
                                     "pinname":  "",
                                     "pinmode":  "input",
                                     "capturemode":  "cyclic-polling",
                                     "inputdebouncetime":  200,
                                     "pwmfrequency":  5000,
                                     "logicactivelow":  false,
                                     "exposetomqtt":  false,
                                     "exposetorest":  false,
                                     "smartled":  {
                                                      "type":  0,
                                                      "quantity":  1,
                                                      "colorredchannel":  255,
                                                      "colorgreenchannel":  255,
                                                      "colorbluechannel":  255
                                                  },
                                     "intensitycorrectionfactor":  100
                                 }
                             ]
             },
    "log":  {
                "debug":  {
                              "loglevel":  1,
                              "logfilesretention":  1,
                              "debugfilesretention":  5
                          },
                "data":  {
                             "enabled":  false,
                             "datafilesretention":  3
                         }
            },
    "network":  {
                    "opmode":  0,
                    "timedoffdelay":  60,
                    "hostname":  "watermeter",
                    "wlan":  {
                                 "ssid":  "",
                                 "password":  "",
                                 "ipv4":  {
                                              "networkconfig":  0,
                                              "ipaddress":  "",
                                              "subnetmask":  "",
                                              "gatewayaddress":  "",
                                              "dnsserver":  ""
                                          },
                                 "wlanroaming":  {
                                                     "enabled":  false,
                                                     "rssithreshold":  -75
                                                 }
                             },
                    "wlanap":  {
                                   "ssid":  "AI-on-the-Edge Device",
                                   "password":  "",
                                   "channel":  11,
                                   "ipv4":  {
                                                "ipaddress":  "192.168.4.1"
                                            }
                               },
                    "time":  {
                                 "timezone":  "CET-1CEST,M3.5.0,M10.5.0/3",
                                 "ntp":  {
                                             "timesyncenabled":  true,
                                             "timeserver":  ""
                                         },
                                 "processstartinterlock":  true
                             }
                },
    "system":  {
                   "cpufrequency":  160
               },
    "webui":  {
                  "httpauth":  {
                                   "authmode":  0,
                                   "username":  "aiote",
                                   "password":  ""
                               },
                  "autorefresh":  {
                                      "overviewpage":  {
                                                           "enabled":  false,
                                                           "refreshtime":  5
                                                       },
                                      "datagraphpage":  {
                                                            "enabled":  false,
                                                            "refreshtime":  60
                                                        }
                                  }
              }
}
```