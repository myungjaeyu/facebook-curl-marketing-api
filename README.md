## Campaign Structure
> Facebook Marketing API

![campaign_structure](https://scontent-icn1-1.xx.fbcdn.net/v/t39.2178-6/851593_516881288424097_1568644600_n.jpg?_nc_cat=0&_nc_eui2=AeHYo5hcsHNfeoKLnJuyOI4uCVoDOjwXbEeWc3FvApAluUXw8WSPtITSJUgBqWIw2r-06BYeqKQ6Ws1ERwuQqc_JbFSsH4fiZqwvnGFeDYhhrg&oh=95017bc47254c4144e8c796c2889a045&oe=5BA9503B)

## API endpoints

| API Name | Endpoint |
| -------- | ------------ |
| Campaign | /campaigns |
| Ad Set | /adsets |
| Ad | /ads |
| Creative | /adcreatives |

---

## Campaign

- **Reading**

```json
curl -X GET \
  -d 'effective_status=["ACTIVE","PAUSED"]' \
  -d "fields=name,objective" \
  -d "access_token=<ACCESS_TOKEN>" \
  https://graph.facebook.com/v3.0/act_<AD_ACCOUNT_ID>/campaigns
```

```json
$ curl -G \
  -d "fields=name,campaign_status" \
  -d "access_token=<ACCESS_TOKEN>" \
  "https://graph.facebook.com/v3.0/<AD_CAMPAIGN_ID>/adcampaigns"
```

```json
$ curl -G \
  -d "fields=id,name,objective" \
  -d "access_token=<ACCESS_TOKEN>" \
  https://graph.facebook.com/v3.0/<CAMPAIGN_ID>/
```

- **Creating**

```json
$ curl -X POST \
     -d "name=My+campaign" \
     -d "objective=LINK_CLICKS" \
     -d "status=PAUSED" \
        https://graph.facebook.com/v3.0/act_<AD_ACCOUNT_ID>/campaigns/
```

- **Updating**

```json
$ curl \
    -F 'name=My new campaign name' \
    -F 'access_token=<ACCESS_TOKEN>' \
    https://graph.facebook.com/v3.0/<CAMPAIGN_ID>/
```

- **Deleting**

```json
$ curl -X DELETE \
    -d 'access_token=<ACCESS_TOKEN>' \
    https://graph.facebook.com/v3.0/<CAMPAIGN_ID>/
```

## AdSet

- **Reading**

```json
$ curl \
    -F 'fields=name' \
    https://graph.facebook.com/v3.0/<AD_CAMPAIGN_ID>/adsets/
```

- **Creating**

```json
$ curl \
  -F 'name=My First AdSet' \
  -F 'lifetime_budget=2000000' \ // 예산
  -F 'start_time=<START_TIME>' \
  -F 'end_time=<END_TIME>' \
  -F 'campaign_id=<CAMPAIGN_ID>' \
  -F 'bid_amount=500' \
  -F 'billing_event=IMPRESSIONS' \
  -F 'optimization_goal=POST_ENGAGEMENT' \
  -F 'targeting={ 
    "age_max": 24, 
    "age_min": 20, 
    "behaviors": [{"id":6002714895372,"name":"All travelers"}], 
    "genders": [1], 
    "geo_locations": { 
      "countries": ["JP"], 
      "regions": [{"key":"3886"}], 
      "cities": [ 
        { 
          "key": "2420605", 
          "radius": 10, 
          "distance_unit": "mile" 
        } 
      ] 
    }, 
    "home_ownership": [{"id":6006371327132,"name":"Renters"}], 
    "interests": [{"id":6003107902433,"name":"Association football (Soccer)"}], 
    "life_events": [{"id":6002714398172,"name":"Newlywed (1 year)"}], 
    "publisher_platforms": ["facebook","audience_network"] 
  }' \
  -F 'status=PAUSED' \
  -F 'access_token=<ACCESS_TOKEN>' \
  https://graph.facebook.com/v2.11/act_<AD_ACCOUNT_ID>/adsets

```

`https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group/adsets/`

## Ad

- **Reading**

```json
$ curl -G \
  -d "fields=name" \
  -d "access_token=<ACCESS_TOKEN>" \
  https://graph.facebook.com/v3.0/<AD_ID>

$ curl -G \
  -d "fields=name" \
  -d "access_token=<ACCESS_TOKEN>" \
  https://graph.facebook.com/v3.0/act_<AD_ACCOUNT_ID | CAMPAIGN_ID | AD_SET_ID>/ads
```

- **Creating**

```json
$ curl \
    -F 'name=My Ad' \
    -F 'adset_id=<AD_SET_ID>' \
    -F 'creative={
          "creative_id":"<CREATIVE_ID>"
        }' \
    -F 'status=PAUSED' \
    -F 'access_token=<ACCESS_TOKEN>' \
    https://graph.facebook.com/v3.0/act_<AD_ACCOUNT_ID>/ads
```

- **Updating**

```json
$ curl \
  -F "name=New Ad Name" \
  -F "access_token=<ACCESS_TOKEN>" \
  https://graph.facebook.com/v3.0/<AD_ID>
```

- **Deleting**

```json
$ curl \
    -F "status=DELETED" \
    -F "access_token=<ACCESS_TOKEN>" \
    https://graph.facebook.com/v3.0/<AD_ID>
```

## Creative

- **Reading**

```json
$ curl -G \
    -d "fields=post_id" \
    -d "access_token=<ACCESS_TOKEN>" \
    https://graph.facebook.com/v3.0/<SPONSOR_PAGE_ID>/bc_sponsored_posts/
```

- **Creating**

`https://developers.facebook.com/docs/marketing-api/guides/videoads`

```json
curl \
  -F 'name=Sample Creative' \
  -F 'object_story_spec={ 
    "link_data": { 
      "child_attachments": [ 
        { 
          "description": "$8.99", 
          "image_hash": "<IMAGE_HASH>", 
          "link": "https:\/\/www.link.com\/product1", 
          "name": "Product 1", 
          "video_id": "<VIDEO_ID>" 
        }, 
        { 
          "description": "$9.99", 
          "image_hash": "<IMAGE_HASH>", 
          "link": "https:\/\/www.link.com\/product2", 
          "name": "Product 2", 
          "video_id": "<VIDEO_ID>" 
        }, 
        { 
          "description": "$10.99", 
          "image_hash": "<IMAGE_HASH>", 
          "link": "https:\/\/www.link.com\/product3", 
          "name": "Product 3" 
        } 
      ], 
      "link": "<URL>" 
    }, 
    "page_id": "<PAGE_ID>" 
  }' \
  -F 'access_token=<ACCESS_TOKEN>' \
  https://graph.facebook.com/v2.11/act_<AD_ACCOUNT_ID>/adcreatives
```

```json
curl \
  -F 'name=Sample Creative' \
  -F 'object_story_spec={ 
    "page_id": "<PAGE_ID>", 
    "video_data": {"image_url":"<THUMBNAIL_URL>","video_id":"<VIDEO_ID>"} 
  }' \
  -F 'access_token=<ACCESS_TOKEN>' \
  https://graph.facebook.com/v2.11/act_<AD_ACCOUNT_ID>/adcreatives
```

```json
curl \
  -F 'slideshow_spec={ 
    "images_urls": [ 
      "<IMAGE_URL_1>", 
      "<IMAGE_URL_2>", 
      "<IMAGE_URL_3>" 
    ], 
    "duration_ms": 2000, 
    "transition_ms": 200 
  }' \
  -F 'access_token=<ACCESS_TOKEN>' \
  https://graph-video.facebook.com/v2.11/act_<AD_ACCOUNT_ID>/advideos
```

```json
curl \
 -F "access_token=<TOKEN>" \
 -F "branded_content_sponsor_page_id=<PAGE_ID>" \
 -F "object_story_id=<OBJECT_STORY_ID" \
https://graph.facebook.com/<VERSION>/<ACCOUNT_ID>/adcreatives
```

```json
curl \
  -F "name=Sample Creative" \
  -F "title=my title" \
  -F "body=my body" \
  -F "object_url=https://www.link.com" \
  -F "link_url=https://www.link.com" \
  -F "image_hash=<IMAGE_HASH>" \
  -F "access_token=<ACCESS_TOKEN>" \
  https://graph.facebook.com/v2.11/act_<AD_ACCOUNT_ID>/adcreatives
```

- **Updating**

```json
$ curl \
  -F 'name=New creative name 1517287' \
  -F 'access_token=<ACCESS_TOKEN>' \
  https://graph.facebook.com/v3.0/<CREATIVE_ID>
```

- **Deleting**

```json
$ curl -X DELETE \
  -d 'access_token=<ACCESS_TOKEN>' \
  https://graph.facebook.com/v3.0/<CREATIVE_ID>
```




| Reference | URL |
| -------- | ------------ |
| Facebook business API | https://developers.facebook.com/docs/marketing-api/reference/v3.0 |