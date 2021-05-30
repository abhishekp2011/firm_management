"# firm_management" 
show tables;
+----------------+
| Tables_in_firm |
+----------------+
| attendance     |
| customer       |
| customer_norm  |
| emp_person     |
| employee       |
| items          |
| man_person     |
| manager        |
| orders         |
| orders_norm    |
| production     |
| sales          |
+----------------+

<!-- show create table attendance; -->

CREATE TABLE `attendance` (
  `emp_id` int NOT NULL,
  `date` date NOT NULL,
  `presence` varchar(20) DEFAULT 'Present',
  PRIMARY KEY (`emp_id`,`date`),
  CONSTRAINT `chk_pres` CHECK ((`presence` in (_utf8mb4'Present',_utf8mb4'Half Day',_utf8mb4'Holiday',_utf8mb4'Absent')))
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table customer; -->

 CREATE TABLE `customer` (
  `customer_id` int NOT NULL AUTO_INCREMENT,
  `first_name` varchar(20) NOT NULL,
  `last_name` varchar(20) DEFAULT NULL,
  `zip_code` char(6) NOT NULL,
  `state` varchar(30) NOT NULL,
  `street_add` varchar(100) DEFAULT NULL,
  `tin_no` varchar(20) DEFAULT NULL,
  `buis_name` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`customer_id`)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table customer_norm; -->

 CREATE TABLE `customer_norm` (
  `customer_id` int DEFAULT NULL,
  `phone` varchar(10) DEFAULT NULL,
  KEY `customer_id` (`customer_id`),
  CONSTRAINT `customer_norm_ibfk_1` FOREIGN KEY (`customer_id`) REFERENCES `customer` (`customer_id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table emp_person; -->

CREATE TABLE `emp_person` (
  `emp_id` int NOT NULL AUTO_INCREMENT,
  `aadhar` char(12) DEFAULT NULL,
  `first_name` varchar(50) NOT NULL,
  `last_name` varchar(50) DEFAULT NULL,
  `doj` date NOT NULL,
  `job` varchar(50) NOT NULL,
  `dob` date NOT NULL,
  `father` varchar(50) DEFAULT NULL,
  `salary` int DEFAULT NULL,
  `layoff` date DEFAULT NULL,
  `password` varchar(50) NOT NULL,
  `state` varchar(50) DEFAULT NULL,
  `pri_phone` char(10) DEFAULT NULL,
  `sec_phone` char(10) DEFAULT NULL,
  PRIMARY KEY (`emp_id`),
  UNIQUE KEY `aadhar` (`aadhar`),
  UNIQUE KEY `pri_phone` (`pri_phone`)
) ENGINE=InnoDB AUTO_INCREMENT=23 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table items; -->

CREATE TABLE `items` (
  `item_id` varchar(20) NOT NULL,
  `description` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`item_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table man_person; -->

 CREATE TABLE `man_person` (
  `man_id` int NOT NULL,
  `aadhar` char(12) DEFAULT NULL,
  `first_name` varchar(50) NOT NULL,
  `last_name` varchar(50) DEFAULT NULL,
  `doj` date NOT NULL,
  `job` varchar(50) NOT NULL,
  `dob` date NOT NULL,
  `father` varchar(50) DEFAULT NULL,
  `salary` int DEFAULT NULL,
  `age` int DEFAULT NULL,
  `layoff` date DEFAULT NULL,
  `password` varchar(50) NOT NULL,
  `zip` char(6) DEFAULT NULL,
  `state` varchar(50) DEFAULT NULL,
  `pri_phone` char(10) DEFAULT NULL,
  `sec_phone` char(10) DEFAULT NULL,
  PRIMARY KEY (`man_id`),
  UNIQUE KEY `aadhar` (`aadhar`),
  UNIQUE KEY `pri_phone` (`pri_phone`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table orders; -->

 CREATE TABLE `orders` (
  `order_id` int NOT NULL AUTO_INCREMENT,
  `customer_id` int NOT NULL,
  `advance` int DEFAULT NULL,
  `status` varchar(10) DEFAULT 'Pending',
  `del_date` date DEFAULT NULL,
  `place_date` date DEFAULT NULL,
  PRIMARY KEY (`order_id`),
  CONSTRAINT `orders_chk_1` CHECK ((`place_date` <= `del_date`))
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table orders_norm; -->

CREATE TABLE `orders_norm` (
  `order_id` int DEFAULT NULL,
  `item_id` varchar(20) DEFAULT NULL,
  `quantity` varchar(20) DEFAULT NULL,
  KEY `order_id` (`order_id`),
  CONSTRAINT `orders_norm_ibfk_1` FOREIGN KEY (`order_id`) REFERENCES `orders` (`order_id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!-- show create table production; -->

CREATE TABLE `production` (
  `item_id` int DEFAULT NULL,
  `quamtity` int DEFAULT NULL,
  `date` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

<!--  show create table sales; -->

 CREATE TABLE `sales` (
  `sales_id` int NOT NULL AUTO_INCREMENT,
  `order_id` int NOT NULL,
  `date` date DEFAULT NULL,
  `status` varchar(20) DEFAULT 'Pending Payment',
  `trans_name` varchar(50) DEFAULT NULL,
  `vehicle_num` varchar(20) DEFAULT NULL,
  `bill` int DEFAULT NULL,
  PRIMARY KEY (`sales_id`),
  UNIQUE KEY `order_id` (`order_id`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
