# MIS
##
MIS homework
管理信息系统作业——设备保养数据模型<br/>
数据表：<br/>
1、保养记录单<br/>
CREATE TABLE `保养记录单` (<br/>
  `保养ID` int(11) NOT NULL,<br/>
  `设备ID` int(11) DEFAULT NULL,<br/>
  `设备名称` varchar(45) DEFAULT NULL,<br/>
  `保养类别` varchar(45) DEFAULT NULL,<br/>
  `保养人` varchar(45) DEFAULT NULL,<br/>
  `保养时间` varchar(45) DEFAULT NULL,<br/>
  `保养内容` varchar(45) DEFAULT NULL,<br/>
  `备注` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养ID`),<br/>
  KEY `保养类别_idx` (`保养类别`),<br/>
  KEY `设备名称_idx` (`设备名称`),<br/>
  KEY `设备ID_idx` (`设备ID`),<br/>
  CONSTRAINT `设备ID` FOREIGN KEY (`设备ID`) REFERENCES `设备` (`设备ID`) ON DELETE NO ACTION ON UPDATE NO ACTION,<br/>
  CONSTRAINT `设备名称` FOREIGN KEY (`设备名称`) REFERENCES `保养消耗` (`设备名称`) ON DELETE NO ACTION ON UPDATE NO ACTION,<br/>
  CONSTRAINT `保养类别` FOREIGN KEY (`保养类别`) REFERENCES `保养类别` (`保养类别`) ON DELETE NO ACTION ON UPDATE NO ACTION,<br/>
  CONSTRAINT `保养ID` FOREIGN KEY (`保养ID`) REFERENCES `保养项目` (`保养ID`) ON DELETE NO ACTION ON UPDATE NO ACTION<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
2、保养类别表<br/>
CREATE TABLE `保养类别` (<br/>
  `保养类别ID` int(11) NOT NULL,<br/>
  `保养类别` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养类别ID`),<br/>
  KEY `保养类别` (`保养类别`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
3、保养消耗表<br/>
CREATE TABLE `保养消耗` (<br/>
  `保养ID` int(11) NOT NULL,<br/>
  `材料ID` int(11) NOT NULL,<br/>
  `消耗材料` varchar(45) DEFAULT NULL,<br/>
  `消耗数量` varchar(45) DEFAULT NULL,<br/>
  `设备名称` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养ID`),<br/>
  KEY `设备名称` (`设备名称`),<br/>
  KEY `材料ID_idx` (`材料ID`),<br/>
  CONSTRAINT `材料ID` FOREIGN KEY (`材料ID`) REFERENCES `材料表` (`材料ID`) ON DELETE NO ACTION ON UPDATE NO ACTION<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
4、保养项目表<br/>
CREATE TABLE `保养项目` (<br/>
  `保养ID` int(11) NOT NULL,<br/>
  `保养设备类型` varchar(45) DEFAULT NULL,<br/>
  `保养设备` varchar(45) DEFAULT NULL,<br/>
  `保养内容` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养ID`),<br/>
  KEY `保养设备类型_idx` (`保养设备类型`),<br/>
  CONSTRAINT `保养设备类型` FOREIGN KEY (`保养设备类型`) REFERENCES `设备类型` (`设备类别`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
5、材料表<br/>
CREATE TABLE `材料表` (<br/>
  `材料ID` int(11) NOT NULL AUTO_INCREMENT,<br/>
  `材料名称` varchar(45) DEFAULT NULL,<br/>
  `材料数量` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`材料ID`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
6、设备表<br/>
CREATE TABLE `设备` (<br/>
  `设备ID` int(11) NOT NULL,<br/>
  `设备类别` varchar(45) DEFAULT NULL,<br/>
  `设备名称` varchar(45) DEFAULT NULL,<br/>
  `最后一次保养时间` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`设备ID`),<br/>
  KEY `设备类别_idx` (`设备类别`),<br/>
  CONSTRAINT `设备类别` FOREIGN KEY (`设备类别`) REFERENCES `设备类型` (`设备类别`) ON DELETE NO ACTION ON UPDATE NO ACTION<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
7、设备类型表<br/>
CREATE TABLE `设备类型` (<br/>
  `设备类别ID` int(11) NOT NULL AUTO_INCREMENT,<br/>
  `设备类别` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`设备类别ID`),<br/>
  KEY `设备类别` (`设备类别`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>

2.查询设备保养信息<br/>
1、SELECT * FROM 设备保养系统.保养记录单<br/>
where 保养ID=(select 保养ID from 设备保养系统.保养消耗<br/>
where 材料ID='1');<br/>
![1](https://github.com/09143793/MIS/blob/master/1.png)
 
2、SELECT * FROM 设备保养系统.保养消耗<br/>
where 材料ID='1';<br/>
![2](https://github.com/09143793/MIS/blob/master/2.png)
 
3、SELECT * FROM 设备保养系统.保养项目<br/>
where 设备ID='1';<br/>
![3](https://github.com/09143793/MIS/blob/master/3.png)
 

/4、Select 设备ID from设备保养系统.设备类型<br/>
Where 365-datediff(now(),(select date from 设备保养系统.保养类别))<6;<br/>
![4](https://github.com/09143793/MIS/blob/master/4.png)
 
ER图模型：<br/>
![ER图](https://github.com/09143793/MIS/blob/master/ER.png)
 
AXURE模型地址：http://5go4q4.axshare.com<br/>
