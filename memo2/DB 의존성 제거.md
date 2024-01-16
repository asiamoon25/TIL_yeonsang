
|  |  |  |
| ---- | ---- | ---- |
| **dataSource_ava** | AvaService | getEventList() |
|  |  | getEventInfo() |
|  |  | getUserEventStatList() |
|  |  | searchClanList() |
|  |  | getClanUserInfo() |
|  |  | getClanUserDetailInfo() |
|  |  | joinClan() |
|  |  | withdrawClan() |
|  |  | mergeClan() |
|  |  | approveClanUser() |
|  |  | rejectClanUser() |
|  |  | getClanUserList() |
|  |  | sendEventItem() |
|  |  | changeRoleClanUser() |
|  |  | blockClan() |
|  |  | getPersonalRankListForArenaRP() |
|  |  | getMonthlyPersonalRankListForExp() |
|  |  | getCumulativePersonalRankListForExp() |
|  |  | getCumulativeClanUserRankInfo() |
|  |  | getClanRankListForArenaRP() |
|  |  | getCumulativeClanRankListForRP() |
|  |  | getMonthlyClanRankListForRP() |
|  |  | getUserMissionAchieveInfo() |
|  |  | getAvaGtUserInfo() |
|  |  | getUserMissionForHomework() |
|  |  | checkDailyCheckCondition() |
| dataSource_ava_ccu | AvaService | getCcu |



cat /var/log/jcgf/api-req/EventsController/preRegist/2024-01-15.txt | grep -E "\[game/12skymori.*" | grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' | sort | uniq -c | sort -nr


악성유저 분류, ip, 핸드폰 번호, agent 
/var/log/jcgf/api-req/EventsController/sendPreRegistjson