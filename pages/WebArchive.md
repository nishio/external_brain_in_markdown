---
title: "WebArchive"
---

python

```
api = "https://web.archive.org/__wb/calendarcaptures/2"


def crawl_year(year):
    r = requests.get(
        f"{api}?url={url}&date={year}&groupby=day")
    days = [x[0] for x in r.json()["items"]]
    for day in days:
        crawl_day(year, day)


def crawl_day(year, day):
    r = requests.get(
        f"{api}?url={url}&date={year}{day:04d}")
    hms_list = [x[0] for x in r.json()["items"]]
    for hms in hms_list:
        crawl_timestamp(year, day, hms)


def crawl_timestamp(year, day, hms):
    timestamp = f"{year}{day:04d}{hms:06d}"
    print(timestamp)
    path = f"quotes/{timestamp}"
    os.makedirs(path)

    print(1)
    r = requests.get(
        f"https://web.archive.org/web/{timestamp}/{url}")
    if r.status_code == 200:
        print(
            "OK",
            open(f"{path}/1.html", "w").write(r.text))
    time.sleep(10)

    for i in range(2, 10000):
        print(i)
        r = requests.get(
            f"https://web.archive.org/web/{timestamp}/{url}?page={i}")
        if r.status_code == 200:
            print(
                "OK",
                open(f"quotes/{i}.html", "w").write(r.text))
        else:
            print("NG", r.status_code)
            break
        time.sleep(10)
```
