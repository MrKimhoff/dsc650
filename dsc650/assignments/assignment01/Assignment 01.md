---
# Taylor Imhof
# Bellevue University | DSC 650
# Assignment 1
# Date: 6/22/2022

---

## 1.2 

#### a. Data Sizes

| Data Item                                  | Size per Item | 
|--------------------------------------------|--------------:|
| 128 character message.                     |     128 Bytes |
| 1024x768 PNG image                         |       3.15 MB |
| 1024x768 RAW image                         |       1.57 MB | 
| HD (1080p) HEVC Video (15 minutes)         |      112.5 MB |
| HD (1080p) Uncompressed Video (15 minutes) |        150 MB |
| 4K UHD HEVC Video (15 minutes)             |      562.5 MB |
| 4k UHD Uncompressed Video (15 minutes)     |        750 MB |
| Human Genome (Uncompressed)                |       0.75 GB |

#### Data size explanations
 - 1 byte per character
 - Images: image file size calculator from [toolstud](https://toolstud.io/photo/filesize.php?imagewidth=1024&imageheight=768)
 - HD Video: assumed bitrate of 10 Mbps and compression ratio of .75
   - formula: file_size = bitrate x duration x compression ration [Source](https://www.circlehd.com/blog/how-to-calculate-video-file-size)
   - uncompressed remove compression ratio in calculation
 - 4K Video: assumed bit bitrate of 50 Mbps and compression ratio of .75
 - Human genome: 3 billion base pairs, each pair coded by 2 bits across 30,000 genes [WikiArticle](https://en.wikipedia.org/wiki/Human_genome#Information_content)
#### b. Scaling

|                                           |      Size | # HD | 
|-------------------------------------------|----------:|-----:|
| Daily Twitter Tweets (Uncompressed)       |    192 GB |    1 |
| Daily Twitter Tweets (Snappy Compressed)  |     96 GB |    1 |
| Daily Instagram Photos                    |    708.75 |    1 |
| Daily YouTube Videos                      |    972 GB |    1 |
| Yearly Twitter Tweets (Uncompressed)      |   70.1 TB |   71 |
| Yearly Twitter Tweets (Snappy Compressed) |  35.04 TB |   36 |
| Yearly Instagram Photos                   | 258.75 TB |  259 |
| Yearly YouTube Videos                     |  254.9 TB |  255 |

#### Scaling explanations
*Multiply every storage by 3 because Hadoop requirements*
 - Tweets
   - 500M daily tweets x 128 Bytes (1 byte per character) = 64 GB/day
   - Snappy compression (1.5x ratio) = 32 GB/day
   - Yearly
     - Uncompressed: 64 GB * 365 = 23.36 TB
     - Snappy: 32 GB * 365 = 11.68 TB
 - Instagram
   - 75,000,000 PNG x 3.15 MB = 236.25 GB/day
   - Yearly:
     - 236.25 GB * 365 = ~86.25 TB
 - YouTube
   - 500 hrs x 1440 (minutes/day) = 720,000 hours of video/day
   - 112.5 MB x 4 = 450 MB/hour of video
   - 450 MB * 720,000 = 324 GB/day
   - Yearly:
     - 324 GB * 365 = ~118.3 TB

#### c. Reliability
|                                    | # HD | # Failures |
|------------------------------------|-----:|-----------:|
| Twitter Tweets (Uncompressed)      |   71 |          9 |
| Twitter Tweets (Snappy Compressed) |   36 |         ~5 |
| Instagram Photos                   |  259 |        ~33 |
| YouTube Videos                     |  255 |        ~32 |

#### Reliability assumptions
 - Used 2021 annualized failure rate of: 1.27% [Backblaze](https://www.extremetech.com/computing/331241-backblaze-publishes-stats-for-hard-drive-failure-in-2021)

#### d. Latency

|                           | One Way Latency |
|---------------------------|----------------:|
| Los Angeles to Amsterdam  |          224 ms |
| Low Earth Orbit Satellite |      594-624 ms |
| Geostationary Satellite   |          400 ms |
| Earth to the Moon         |        2.56 sec |
| Earth to Mars             |       ? minutes | 

#### Latency explanations
 - Used latency estimator from ConsoleConnect website [Source](https://www.consoleconnect.com/locations/amsterdam/)
 - LEO Satellite: average satellite internet between 594 ms to 624 ms [Source](https://www.satelliteinternet.com/resources/gaming-on-satellite-internet/)
 - GEO Satellite: end-to-end latency as high as 400 ms [Source](https://web.archive.org/web/20160103125227/https://www.isoc.org/inet97/proceedings/F5/F5_1.HTM#:~:text=For%20GEO%20satellite%20communications%20systems,as%20high%20as%20400%20milliseconds).)
 - Propagation time to moon and back is 2.56 seconds
   - one-way travel would be half that
 - Earth to Mars: between 5 and 20 minutes depending on planetary positions [NASA](https://mars.nasa.gov/mars2020/spacecraft/rover/communications/#:~:text=It%20generally%20takes%20about%205,Earth%2C%20depending%20on%20planet%20positions.)