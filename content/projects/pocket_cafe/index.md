---
title: "Pocket Café: Your favorite cafés in your pocket!"
date: 2022-06-01
draft: true
project_tags: ["coffee", "Heroku", "LINE Messaging API", "PostgreSQL", "Python", "Vue.js", "node.js"]
status: "evergreen"
weight: 3
summary: "A simple LINE Bot to find the nearest Café!"
---

# Pocket Café: Your favorite cafés in your pocket!

Tags: Heroku, LINE Messaging API, PostgreSQL, Python, Vue.js, node.js

Short summarization in English by ChatGPT.

As a former member of a coffee society, I've always been passionate about coffee. I enjoy visiting various cafes to explore new flavors and chat with the owners about brewing and roasting techniques. When I'm at a cafe, I often read or work, relishing the personal time. My main objective was to develop an application that could quickly and easily provide information about cafes. I realized that Google Maps, while useful, often suggested places like restaurants that serve coffee, rather than actual cafes.

In my search for a better solution, I discovered [Cafe Nomad]((https://cafenomad.tw/)), a website that uses crowdsourcing to list over 3,000 Taiwanese cafes, complete with user ratings on several aspects, like coffee quality and availability of WiFi. However, the site's standalone nature and its overwhelming presentation of cafes made it less user-friendly.

To improve this, I created a LINE Bot and a website that, when given a location, returns information about the seven nearest cafes. It also allows users to explore top-rated cafes in different counties, save and delete favorite cafes, all within LINE, and share their list of favorite cafes through the website.

Chinese version of the report below.

# 1. Motivation

## 出發點: Coffee and Café

身為一個咖啡社的前社幹，我非常的喜歡喝咖啡。

除了自己會在家裡和社團沖煮之外，我時不時也喜歡到不同的**咖啡廳**探索新的風味，和店家聊聊天、切磋沖煮與烘豆的技巧，而在品味咖啡的同時，我也會選擇待在咖啡廳念書或工作，享受個人的時光。所以在沒課的時候，我會選一間**沒去過**咖啡廳探險，品嘗不同的風味。如果找到不錯的，我也會和咖啡社的朋友們分享，或是也推薦周邊有興趣的朋友們去。

而除了喝咖啡之外，其他人找尋咖啡廳的動機也許比我單純：在忙碌的生活中會想換一個環境工作、念書，或只是想到咖啡廳休息一下，看個書。對於這些人來說，「**咖啡廳**」本身才是首要目的，咖啡好不好倒不那麼重要。

雖然動機不同，但對於我們來說，我們都有一個共同目標——我們希望可以有系統地找到不錯的咖啡廳。

**目標**

因此，能夠創造出一個 **1.迅速 且 2.方便 地獲得到咖啡廳的資訊的應用**便成為了我的**首要目標，**若能夠結合**3.收藏、儲存地點**、**4.分享**的功能，那肯定是更好。

## 類似產品

看到這裡，一般人可能會覺得：使用 Google Maps 並輸入「咖啡」就能做到這件事。然而，Google 地圖雖然資訊豐富，卻不會是我平常主要「尋找」咖啡廳的方式。因為往往 Google Maps 會更趨向於推薦有提供咖啡的餐廳、簡餐店給我，而不是確確實實的咖啡廳：Google Maps 對於要有系統性的找到「真正的」咖啡廳還是有一定的難度。

所以我便轉而去尋找一個收錄全台灣咖啡廳的資料集或網站，（這是比寫爬蟲爬遍 Google Maps 的「咖啡廳」還要好的方案）。

## 資料來源

在尋找**資料來源時**，我找到了 [Cafe Nomad](https://cafenomad.tw/) 這個網站，他藉由 crowdsourcing 的方式收錄了全台灣超過 3000 間的咖啡廳，並提供了用戶們對於咖啡廳各項指標的評價：包含咖啡好不好喝、有無插座、有無限時、是否有 WiFi 等等，此外，內容還包括了店家的官網網址以及經緯度。在了解之後，我認為這個網站的資料非常符合我的需求。

我認為這個網站存在的問題在於：

由於他本身是一個獨立的網站（只有網站、沒有app），且需要登入才能夠做更多事情（例如收藏與儲存地點），另外因為一次就呈現 100~200 間咖啡廳，很難讓使用者從中挑選。因此我決定基於這個網站所擁有的資料去做一些改善。

## 最終想法

在思考和發散後的結果，我最後實作出了一個 LINE Bot 和與其搭配的網站，他能夠：

1. 在使用者提供定位位置後，回傳給距離使用者所提供之位置最近的7間咖啡廳的資訊
2. 探索各縣市綜合評價最高的咖啡廳
3. 收藏與刪除喜歡的咖啡廳，全部都在 LINE 中搞定
4. 利用網站的形式將使用者的收藏清單分享給其他人 

由於人人都有LINE，因此改善了上述需要特別辦帳號的問題。此外，因為在LINE裡面就可以將想做的事情搞定，所以便利性也大大提升了。

以下詳述功能與開發過程。

# 2. Application description

## **Pocket Café: Your favorite cafés in your pocket!**

**口袋咖啡廳名單！**

<img class="mw-100" src="assets/featured.jpeg" alt="overview">

## A. 應用描述

只要打開 LINE ，加入 Pocket Café 的好友，就能夠尋找距離您最近的咖啡廳的相關資訊。看到喜歡的店，也能夠收藏起來和朋友們分享。

大功能如第一段所述，在這裡再描述一次

1. 在使用者提供定位位置後，回傳給距離使用者所提供之位置最近的7間咖啡廳的資訊
2. 探索各縣市綜合評價最高的咖啡廳
3. 收藏與刪除喜歡的咖啡廳，全部都在 LINE 中搞定
4. 利用網站的形式將使用者的收藏清單分享給其他人 

LINE Bot QR Code: 歡迎加入好友！

<img class="mw-100" src="assets/Untitled.png" alt="qr-code">

Bot ID: @973cexqv

## B. 功能簡介

### 1. **主頁**

<img class="mw-100" src="assets/73C9400C-B875-4077-B3CA-12F1D2D688AF.jpeg" alt="main-page">

描述應用程式的各個資訊，可點選卡片中的任意區塊繼續。

### 2. **尋找附近的咖啡廳**


<img class="img-fluid" src="assets/55A42F41-2F5F-45ED-9D12-E03D84663B1B.jpeg" alt="near-cafes" style="">

透過傳送地點給 Pocket Cafe，Bot 會回傳距離地點最近的7間咖啡廳以及下列資訊：

- 距離：咖啡廳距離給定的位置的距離
- 地址、營業時間
- 地圖資訊：點選地圖縮圖即可打開 Google Maps 導航，地圖縮圖有呈現起點與終點間的最短直線距離

<img class="mw-100" src="assets/Untitled%201.png" alt="map-info"> 

- 店家各項機能評價
- View On Cafe Nomad：更多詳細資訊 (導向外部網站)

<img class="img-fluid" src="assets/E439078A-B451-49EB-BBAD-30BE97FA70C0.jpeg" alt="external-link" style="">
    
- Official Site: 若有官方網站資訊，也可前往

### 3. 收藏咖啡廳

- 點選儲存地點，即可收藏咖啡廳。

<img class="img-fluid" src="assets/242A33C5-D3C0-402F-A1E6-7081578936B2.jpeg" alt="save-cafe"
    style="">

- 點選「我的咖啡廳清單」，可查看已儲存的所有咖啡廳

<img class="img-fluid" src="assets/1D3D1BEA-9F9A-4B9F-B17A-DF5F6552D11C.png" alt="my-cafe-list"
    style="">

- 點選「移除地點」自收藏清單刪除咖啡廳

### 4. 探索地區綜合評價最高的咖啡廳

可以探索各地區：新竹、台北、台南、高雄，根據 Cafe Nomad 上綜合評價排名前十高的咖啡廳。

### 5. 分享自己收藏的咖啡廳

點選主頁的「分享我的收藏」可將儲存的咖啡廳清單**生成一個網頁**，透過此網頁即可和朋友們分享自己喜歡的咖啡廳。


<img class="img-fluid" src="assets/33CD3331-F75D-4240-B38A-22AB44E1E15F.png" alt="share-link"
    style="">

範例如：[https://pocket-cafe.herokuapp.com/lists/U18117193e4b725a34c17dbe69ebca882](https://pocket-cafe.herokuapp.com/lists/U18117193e4b725a34c17dbe69ebca882)

## C. 技術架構
<div class="row">
    <div class="col-12 col-md-6">
        <img class="img-fluid" src="assets/Untitled%202.png" alt="line-msg-platform">
    </div>
    <div class="col-12 col-md-6">
        <img class="img-fluid" src="assets/Untitled%204.png" alt="google-maps">
    </div>
    <div class="col-12 col-md-6">
        <img class="img-fluid" src="assets/Untitled%203.png" alt="amazon-rds">
    </div>
    <div class="col-12 col-md-6">
        <img class="img-fluid" src="assets/Untitled%205.png" alt="heroku">
    </div>
    <div class="col-12 col-md-6">
        <img class="img-fluid" src="assets/Untitled%206.png" alt="nuxtjs">
    </div>
    <div class="col-12 col-md-6">
        <img class="img-fluid" src="assets/Untitled%207.png" alt="nodejs">
    </div>
</div>

**Front-end:**

[LINE messaging API](https://developers.line.biz/en/reference/messaging-api/) for interacting with LINE

[Google Maps API](https://developers.google.com/maps/documentation/maps-static/) to generate static map images

**Front-end Website:**

Website written in [Nuxt.js](https://nuxtjs.org/), hosted on Heroku

**Backend:** hosted on Heroku

Node.js and express.js for server management

[node-postgres](https://node-postgres.com/) for interfacing with PostgreSQL

**Database:** PostgreSQL, hosted on Amazon RDS


**Github repo:**

Frontend: [https://github.com/newb1er/PocketCafeListWeb](https://github.com/newb1er/PocketCafeListWeb)

Kudos to my friend 簡右群 for helping me out to setting up the front-end framework!

Backend: [https://github.com/andyrochi/PocketCafeList](https://github.com/andyrochi/PocketCafeList)

For both the LINE bot server and backend API

我們主要將處理所有 request 的 server 部署在 Heroku 提供的服務上面，這部分是由 nodejs 寫成。Server會同時收到前端頁面以及 LINE messaging API 的請求，server再根據請求由資料庫獲取資料或是直接回覆。

# 3. Data sources and How it is collected

## 咖啡廳資訊

如同，前文所述， Cafe Nomad 的資料非常適合我們利用。

<img class="img-fluid" src="assets/Untitled%208.png" alt="cafe-nomad-src">

而其剛好有提供[API](https://cafenomad.tw/developers/docs/v1.2)，因此我們就直接由 API 取得資料並存入資料庫即可。

目前共有3446間咖啡廳。

在經過分析後，內含欄位為：

- id - 一組UUID：string
- name - 店名：string
- wifi - wifi 穩定：float, 0.0~5.0的值
- seat - 通常有位：float, 0.0~5.0的值
- quiet - 安靜程度：float, 0.0~5.0的值
- tasty - 咖啡好喝：float, 0.0~5.0的值
- cheap - 價格便宜：float, 0.0~5.0的值
- music - 裝潢音樂：float, 0.0~5.0的值
- address - 地址：string
- latitude - 緯度
- longitude - 經度
- url - 官網：string
- limited_time - 有無限時：string, yes/maybe/no/null
- socket - 插座多：string, yes/maybe/no/null
- standing_desk - 可站立工作：string, yes/no/null
- mrt - 捷運站：string, 有關捷運站的資訊
- open_time - 營業時間：string

根據我的理解，店家資訊不會變動太快，因此不須要短時間內一直更新，大約一週更新一次即可。

因此，我們首先根據欄位資訊建好一個table。接著再使用 `node.js` 先從 API 請求資料，再使用`node-postgres` 將每一個欄位`INSERT`進database。

SQL 指令為：

```sql
INSERT INTO cafe(id,name,city,wifi,seat,quiet,tasty,cheap,music
								,url,address,latitude,longitude,limited_time,socket,standing_desk,mrt,open_time) 
						VALUES (....);
```

## 用戶資訊

使用 LINE Messaging API，用戶傳的每一條訊息都會附帶 userId，我們可以藉此辨別訊息傳送者的身分，然而卻無法得知使用者的名稱。

LINE 有另一個 API 能夠取得使用者的名稱，因此在使用者剛加入 LINE Bot 為好友時，我們便藉由此API 獲取使用者的資訊，並與 userid 一同存入 user table 中。

## 用戶的收藏清單

使用者於使用我們的 Bot 時自然會新增與刪除資料，因此我們只須先將 table 建好即可。

# 4. Database schema

## ERD generated by pgAdmin:

<img class="img-fluid" src="assets/Untitled%209.png" alt="erd-diagram">

Tables:
- cafe
- user
- saved_location

## Table 1: cafe

此 table 主要都與咖啡廳 cafe 有關，且所有的 attribute 都是 functionally dependent on id (Primary Key)，再加上我能想到的 query 幾乎都是一次 request 所有的資訊，因此我就沒有再做後續的拆分。

這個 table 相對單純，根據資料的性質，我將內容用以下的方式儲存，並分別加上了 NOT NULL 以及 Primary key 的 constraint。

### Table creation

```sql
CREATE TABLE cafe(
   id            VARCHAR(36) NOT NULL PRIMARY KEY
  ,name          VARCHAR(50)
  ,city          VARCHAR(10) NOT NULL
  ,wifi          NUMERIC(3,1) NOT NULL
  ,seat          NUMERIC(3,1) NOT NULL
  ,quiet         NUMERIC(3,1) NOT NULL
  ,tasty         NUMERIC(3,1) NOT NULL
  ,cheap         NUMERIC(3,1) NOT NULL
  ,music         NUMERIC(3,1) NOT NULL
  ,url           VARCHAR(300)
  ,address       VARCHAR(100)
  ,latitude      NUMERIC(11,8) NOT NULL
  ,longitude     NUMERIC(12,8) NOT NULL
  ,limited_time  VARCHAR(5)
  ,socket        VARCHAR(5)
  ,standing_desk VARCHAR(3)
  ,mrt           VARCHAR(250)
  ,open_time     VARCHAR(300)
);
```

### Constraints

Primary Key: `id`

### Indexing

因為我們的 query 有幾個會 focus 在特定的 city，因此我為 city 加上了 index。

而因為 primary key 在 postgresql 中會預設 index，並當成 clustered index，因此我沒有另外做調整。

## Table 2: user

此 table 主要用於儲存用戶的名稱，由於 `userid`是 unique 的，因此我將其設為 primary key。用戶名稱則依狀況存入，沒有設 constraints。

## Table 3: saved_location

saved_location 是用於紀錄用戶的清單，最常被使用的用途應該是與其他 table 的 natural join。Constraints資訊如下：

### Table creation

```sql
CREATE TABLE public.saved_location
(
    userid character varying(100) NOT NULL,
    id character varying(36) NOT NULL,
		add_date TIMESTAMPTZ NOT NULL,
    CONSTRAINT "PRIMARY_KEY" PRIMARY KEY (userid, id),
    CONSTRAINT "user" FOREIGN KEY (userid)
        REFERENCES public."user" (userid) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
        NOT VALID,
    CONSTRAINT cafe FOREIGN KEY (id)
        REFERENCES public.cafe (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
        NOT VALID
);
```

### Constraints

**Primary key constraints**

- `CONSTRAINT "PRIMARY_KEY" PRIMARY KEY (userid, id)`

**Foreign key constraints**

- `CONSTRAINT "user" FOREIGN KEY (userid) REFERENCES public."user" (userid)`
- `CONSTRAINT cafe FOREIGN KEY (id) REFERENCES public.cafe (id)`

### Indexing

- Primary key 的 indexing 已經很有利於我們的 query 用途

# 5. Application’s functions and the related SQL queries used for the function

## 5-1. Fetching 7 nearest cafes given a location 獲取最近的7間咖啡廳

第一件要解決的事情是如何計算距離，在這裡，我在 pgAdmin 定義了以下的 function 來計算距離：

```sql
CREATE OR REPLACE
FUNCTION calculate_distance(lat1 float, lon1 float, lat2 float, lon2 float, units varchar)
RETURNS float AS $dist$
DECLARE
	dist float = 0;
	radlat1 float;
	radlat2 float;
	theta float;
	radtheta float;
  BEGIN
      IF lat1 = lat2 AND lon1 = lon2
          THEN RETURN dist;
      ELSE
          radlat1 = pi() * lat1 / 180;
          radlat2 = pi() * lat2 / 180;
          theta = lon1 - lon2;
          radtheta = pi() * theta / 180;
          dist = sin(radlat1) * sin(radlat2) + cos(radlat1) * cos(radlat2) * cos(radtheta);

          IF dist > 1 THEN dist = 1; END IF;

          dist = acos(dist);
          dist = dist * 180 / pi();
          dist = dist * 60 * 1.1515;

          IF units = 'K' THEN dist = dist * 1.609344; END IF;
          IF units = 'N' THEN dist = dist * 0.8684; END IF;

          RETURN dist;
      END IF;
  END;
```

傳入參數’K’的話，function的輸出及為兩組經緯度的距離，以公里計算。

我們則只須要使用下列的 SQL query 即可取得距離最近的 7 間咖啡廳。

`$1, $2`為 node-postgres 傳入的參數，即現在的 latitude, longitude。

```sql
SELECT id, 
      name,
      address, 
      open_time, 
      url,
      tasty::float,
      socket,
      limited_time,
      wifi::float,
      latitude::float, 
      longitude::float,
      calculate_distance($1, $2, latitude, longitude, 'K') as distance
FROM cafe
ORDER BY distance
limit 7
```

## 5-2. New user 新用戶加為 LINE 好友，將用戶加入資料庫

在有新用戶加入後，我們的資料庫必須被更新。

我們會先在 node.js 的環境下暫存一些 local 的變數當成cache來判斷這個使用者是否已經出現過，如果有的話就不會做後續的 query。

但如果沒有的話，就代表使用者有兩種可能：

1. 他是新用戶，未被加入資料庫
2. 後端重啟了，cache無此用戶的資料，但用戶資料已經在資料庫裡

這兩種狀況我們都可以用以下的 SQL query 解決：

```sql
INSERT INTO "user"(userid, displayname)
  VALUES($1, $2)
  ON CONFLICT(userid) DO NOTHING
```

在 primary key 有 conflict 的時候 (通常是 unique constraint 的 conflict) 我們就什麼都不做。

## 5-3. Showing the username in the webpage 於網頁中顯示用戶名稱

<img class="img-fluid" src="assets/Untitled%2010.png" alt="username">

由於網頁不是 LINE 的環境，因此我們會需要另外從 database 取得用戶資料。

在這裡，我們從 LINE Bot 將 userid 以參數的方式傳給前端網頁，前端再根據 userid query 後端與資料庫取得對應資訊。

```sql
SELECT * FROM "user" WHERE userid = $1
```

## 5-4. Returning a user’s cafe list 獲取使用者的清單

要取得一個用的清單，我們只需要先以 `userid` 篩選 saved_location 中的 `rows`，再藉由 `natural join` cafe 的 table 即可。

這裡我希望以加入的時間降冪排序。

```sql
WITH saved AS
  (SELECT *
  FROM "saved_location"
  WHERE userid = $1)
  SELECT *
FROM saved NATURAL JOIN cafe
ORDER BY add_date DESC
```

這個 query 同時適用於**產生分享收藏的網頁**，以及於 LINE 列出儲存的咖啡廳。

## 5-5. Adding a new café to saved list 儲存新的咖啡廳至收藏

與新增新用戶的邏輯相同，避免 conflict 的話我們只需要 DO NOTHING 即可。

```sql
INSERT INTO "saved_location"(userid, id, add_date)
  VALUES($1, $2, $3)
  ON CONFLICT DO NOTHING
```

**Miscellaneous details:**

在點下儲存咖啡廳後，由於接收 request 的後端只有咖啡廳的 id，因此我們必須再另外 query database 才能夠取得更多咖啡廳的資訊（如咖啡廳名稱、地址等等），讓使用者使用者體驗更好：

<img class="img-fluid" src="assets/242A33C5-D3C0-402F-A1E6-7081578936B2.jpeg" alt="improvement" style="">

再次 query 的指令如下：

```sql
SELECT * FROM cafe WHERE id = $1
```

## 5-6. Deleting a café from saved list 刪除收藏清單的咖啡廳

我們只需要 userid 與 咖啡廳的 id 即可鎖定一個 unique 的 row（因為是 primary key），因此下列的 query 可以達成我們的目的。

```sql
DELETE FROM saved_location
WHERE userid = $1 AND id = $2
```

## 5-7. Obtaining 10 cafes with the best overall score 取得單一城市綜合評分最高的10間咖啡廳

將咖啡廳按照綜合評分最高至最低排序，並篩選特定城市作為條件， query 的程式碼如下。

```sql
SELECT *, wifi+seat+quiet+tasty+cheap+music AS total
FROM cafe
WHERE city=$1
ORDER BY total DESC
LIMIT 10
```

# 6. Conclusion

經過這次的 project，讓我體驗了從一個專案的發想、到逐漸成形，到最後實作的過程。結合以前在課堂所學的 AWS RDS 和資料庫的知識，再加上不斷的查 document 東拼西湊寫了一個 LINE Bot、研究如何使用 Google Maps API 生成地圖、node.js 寫了後端並串接了 PostgreSQL、用 Vue 寫了一個前端的網頁、並將所有的服務部署到 Heroku/AWS 上供人使用，實在是挺有成就感的。
