##  部署
```shell
docker run --name postgres -e POSTGRES_PASSWORD=123456 -e POSTGRES_USER=postgres   -d -p 5432:5432 postgres


psql -U postgres -W


\l：列出所有数据库。
\c [database_name]：连接其他数据库。
\d：列出当前数据库的所有表格。


两个表 

表一  build_config
Build_Config_Name  BuildID  
one                1                 
two                2
three              3


INSERT INTO build_config (build_config_name, build_id) VALUES ('one',1 );
INSERT INTO build_config (build_config_name, build_id) VALUES ('two',2 );
INSERT INTO build_config (build_config_name, build_id) VALUES ('three',3 );



表二 build
build_name  build_id  timestamp  
one1        1           now-2
one2        1           now-1
two1        2           now
two2        2           now+1
three1      3           now+2
three3      3           now+3
```


INSERT INTO build (build_name, build_id) VALUES ('one1',1 );
INSERT INTO build (build_name, build_id) VALUES ('one2',1 );
INSERT INTO build (build_name, build_id) VALUES ('two1',2 );
INSERT INTO build (build_name, build_id) VALUES ('two2',2 );
INSERT INTO build (build_name, build_id) VALUES ('three1',3 );
INSERT INTO build (build_name, build_id) VALUES ('three2',3 );


INSERT INTO build (timestamp) WHERE build_name='one1' VALUES (current_timestamp);
INSERT INTO build (timestamp) VALUES (current_timestamp);
INSERT INTO build (timestamp) VALUES (current_timestamp);
INSERT INTO build (timestamp) VALUES (current_timestamp);
INSERT INTO build (timestamp) VALUES (current_timestamp);
INSERT INTO build (timestamp) VALUES (current_timestamp);


UPDATE build SET timestamp = current_timestamp WHERE build_name = 'three2';
UPDATE build SET timestamp = current_timestamp WHERE build_name = 'one1';
UPDATE build SET timestamp = current_timestamp WHERE build_name = 'three1';
UPDATE build SET timestamp = current_timestamp WHERE build_name = 'one2';
UPDATE build SET timestamp = current_timestamp WHERE build_name = 'two1';
UPDATE build SET timestamp = current_timestamp WHERE build_name = 'two2';




hope: 3 1 2




从 build 表中获取 并且按照时间排序   再使用in 找出所有的buildconfig


select * from build where (id in select * from build_config) orderby buildTime DESC LIMIT 1;

select Build_Config_Name from buildconfig where BuildID =  (select buildID from build where (id in select * from build_config) orderby buildTime DESC LIMIT 1);
或者是做表链接





找出build中每一条 build_config 对应 timestamp 最大的那个

makerar

 cname  | wmname |          avg           
--------+-------------+------------------------
 canada | zoro   |     2.0000000000000000
 spain  | luffy  | 1.00000000000000000000
 spain  | usopp  |     5.0000000000000000



SELECT m.cname, m.wmname, t.mx
FROM (
    SELECT cname, MAX(avg) AS mx
    FROM makerar
    GROUP BY cname
    ) t JOIN makerar m ON m.cname = t.cname AND t.mx = m.avg
;

 cname  | wmname |          mx           
--------+--------+------------------------
 canada | zoro   |     2.0000000000000000
 spain  | usopp  |     5.0000000000000000


select (build.build_id),MAX(build.timestamp) FROM build GROUP BY build.build_id;



select (build.build_id),MAX(build.timestamp) FROM build GROUP BY build.build_id ORDER BY MAX(build.timestamp);





select build_config.build_config_name FROM build,build_config 
WHERE build.build_id=build_config.build_id 
GROUP BY build_config.build_config_name 
ORDER BY MAX(build.timestamp);