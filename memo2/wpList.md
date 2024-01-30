wpList 있는 곳 CommonMenuPrepare 349 line, 363
```java
Object wpListCache = Memcached.getInstance().get("wpListCache" + game.get("serviceCode"));  
  
if (wpListCache == null) {  
wpList = happycodeSao.GetContentArticleListJSON(request, 1, 30, ProjectConstant.CONTENT_TYPE_WALL_PAPER, gname, true);  
if (UtilObject.isNotNullList(wpList)) {  
Memcached.getInstance().set("wpListCache" + game.get("serviceCode"), Memcached.EXPIRE_1_MINUTE, wpList);  
}  
} else {  
wpList = (List<Map<String, Object>>) wpListCache;  
}  
} catch (Exception e) {  
e.printStackTrace();  
}
```
내일 소호강호 캐시 처리 안됬다고 말하고 캐시처리하기

```java
List<Map<String, Object>> guidekeywordList = null;

Object guidekeywordListCache = Memcached.getInstance().get("guidekeywordListCache" + game.get("serviceCode"));

if(guidekeywordList == nul) {
guidekeywordList = cmsSao.GetContentArticleKeywordJSON(request, CONTENT_TYPE_GUIDE, game.get("serviceCode").toString());
if(UtilObject.isNotNullList(guidekeywordList)) {
Memcached.getInstance().set("guidekeywordListCache"+game.get("serviceCode"), Memecached.EXPIRE_1_MINUTE,guidekeywordList);
}
}else {
guidekeywordList = (List<Map<String,Object>>) guidekeywordListCache;
}
} catch (Exception e) {
e.printStackTracce();
}
```
