# Command to generate load on the ALB

[class 36](http://udemy.com/course/aws-certified-developer-associate-exam-training/learn/lecture/43290798#overview)

***replace with your alb dns name***
```for i in {1..200}; do curl http://your-alb-address.com & done; wait```



```bash
for i in {1..1000}; do  curl 'https://clownfish-app-6bjip.ondigitalocean.app/api/shorten' \
  -H 'accept: */*' \
  -H 'accept-language: en' \
  -H 'authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJsbWVkaW5hZW5jYWxhZGFAbWl1LmVkdSIsImlhdCI6MTc1NDk0NTI1MCwiZXhwIjoxNzU1MDMxNjUwfQ.uns49z1LjFNXqD23e3a_fjyB6suYrFc3Dr98CADnZS0' \
  -H 'content-type: application/json' \
  -H 'origin: https://babyurl.tech' \
  -H 'priority: u=1, i' \
  -H 'referer: https://babyurl.tech/' \
  -H 'sec-ch-ua: "Not)A;Brand";v="8", "Chromium";v="138", "Google Chrome";v="138"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: cross-site' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36' \
  --data-raw '{"url":"https://fitsstream.com/payment/basic?cid=4qEGRMHoq2neKg9RK2MgdU&email=leomedinae.sc@gmail.com&password=123456789&subid=c1889&pubid=p4822&name=leomedina&link_parameters%5Bnid%5D=2&link_parameters%5Bkw%5D=The+System+Design+Interview++2nd+Edition.pdf&link_parameters%5Bcid%5D=1889","userId":1}' & done; wait 
```

