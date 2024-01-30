```shell
#!/bin/sh
INPUT_FILE="/home/happytuk/log_add_xa_preregist.log"
if [ ! -f "$INPUT_FILE" ];then
        touch /home/happytuk/log_add_xa_preregist.log
fi
cat /var/log/jcgf/api-req/EventsController/sendPreRegistjson/2024-01-16.txt > log_add_xa_preregist.log
wait
#cat /var/log/jcgf/api-req/EventsController/sendPreRegistjson/2024-01-15.txt >> log_add_xa_preregist.log
echo "done"
exit 0
```
1. 먼저  target 시간대의 로그를 새로운 파일에 넣는다.
```shell
#!/bin/sh

## 로그 추출

INPUT_FILE="/home/happytuk/log_extraction_ip_address.log"

if [ ! -f "$INPUT_FILE" ];then
        touch $INPUT_FILE
fi

#cat /home/happytuk/log_add_xa_preregist.log | grep -E "\[game/12skymori.*" | awk '{print $3}' | awk -F'\\]\\[' '{print $2}' | sort | uniq -c | sort -nr > $INPUT_FILE

cat /home/happytuk/log_add_xa_preregist.log |grep -E "\[game/12skymori.*" |awk -F'[][]' '{print $8, $13, $15}' | sort | uniq -c | sort -nr >> $INPUT_FILE

echo 'done'
```
log_extraction_ip_address.log 로 count, ip, phone_num, 국가 번호 를 추출 해서 새로운 파일에 넣는다.

끝


IP 로 국가 추출
 geoip 설치
 ```shell
 sudo yum -y install geoip geoip-data
```
shell 작성
```shell
#!/bin/sh

IP_FILE="/home/happytuk/jcgf_777.log"

touch /home/happytuk/ip_address_result.log

cat $IP_FILE | awk '{print $2}'  > /home/happytuk/test.log

wait 

while IFS= read -r ip
do
        country=$(geoiplookup $ip | head -n 1 |awk -F ': ' '{print $2}'| awk -F',' '{print $1}')
        echo $country >> /home/happytuk/ip_address_result.log
        #echo $country 
        #echo $ip
done < "/home/happytuk/test.log"
```
끝