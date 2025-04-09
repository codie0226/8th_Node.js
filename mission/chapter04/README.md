1. 테이블 생성 결과
    
    ERD cloud에서 생성한 DDL을 기반으로 SQL을 자동 생성하고 만들었다.
    
    ```sql
    SET sql_mode='';
    
    CREATE TABLE `mission` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `user_id` INT NOT NULL,
        `shop_id` INT NOT NULL,
        `content` TEXT NULL,
        `point` INT NULL,
        `created_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        `updated_at` TIMESTAMP NULL ON UPDATE CURRENT_TIMESTAMP,
        `status` TINYINT NOT NULL DEFAULT 1,
        PRIMARY KEY (`id`),
        FOREIGN KEY (`user_id`) REFERENCES `user` (`id`) ON DELETE CASCADE,
        FOREIGN KEY (`shop_id`) REFERENCES `shop` (`id`) ON DELETE CASCADE
    );
    
    CREATE TABLE `user` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `username` VARCHAR(20) NULL,
        `gender` TINYINT NULL,
        `address` VARCHAR(50) NULL,
        `email` VARCHAR(30) NULL UNIQUE,
        `phone_number` VARCHAR(20) NULL UNIQUE,
        `point` INT NOT NULL DEFAULT 0,
        PRIMARY KEY (`id`)
    );
    
    CREATE TABLE `shop` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `shop_category` INT NOT NULL,
        `area_id` INT NOT NULL,
        `shop_name` VARCHAR(20) NOT NULL,
        `shop_address` VARCHAR(50) NOT NULL,
        PRIMARY KEY (`id`),
        FOREIGN KEY (`shop_category`) REFERENCES `shop_category` (`id`) ON DELETE CASCADE,
        FOREIGN KEY (`area_id`) REFERENCES `area` (`id`) ON DELETE CASCADE
    );
    
    CREATE TABLE `shop_category` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `category` VARCHAR(10) NOT NULL,
        PRIMARY KEY (`id`)
    );
    
    CREATE TABLE `alarm` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `user_id` INT NOT NULL,
        `alarm_title` TEXT NOT NULL,
        `alarm_content` TEXT NULL,
        `created_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        `updated_at` TIMESTAMP NULL ON UPDATE CURRENT_TIMESTAMP,
        PRIMARY KEY (`id`),
        FOREIGN KEY (`user_id`) REFERENCES `user` (`id`) ON DELETE CASCADE
    );
    
    CREATE TABLE `review` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `user_id` INT NOT NULL,
        `shop_id` INT NOT NULL,
        `review_title` TEXT NOT NULL,
        `review_content` TEXT NOT NULL,
        `review_stars` TINYINT NULL DEFAULT 0,
        `created_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        `updated_at` TIMESTAMP NULL ON UPDATE CURRENT_TIMESTAMP,
        PRIMARY KEY (`id`),
        FOREIGN KEY (`user_id`) REFERENCES `user` (`id`) ON DELETE CASCADE,
        FOREIGN KEY (`shop_id`) REFERENCES `shop` (`id`) ON DELETE CASCADE
    );
    
    CREATE TABLE `user_food_category` (
        `user_id` INT NOT NULL,
        `food_id` INT NOT NULL,
        PRIMARY KEY (`user_id`, `food_id`),
        FOREIGN KEY (`user_id`) REFERENCES `user` (`id`) ON DELETE CASCADE,
        FOREIGN KEY (`food_id`) REFERENCES `food_category` (`id`) ON DELETE CASCADE
    );
    
    CREATE TABLE `food_category` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `food` VARCHAR(10) NOT NULL,
        PRIMARY KEY (`id`)
    );
    
    CREATE TABLE `area` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `area_name` VARCHAR(10) NOT NULL,
        PRIMARY KEY (`id`)
    );
    
    CREATE TABLE `user_area_mission` (
        `id` INT NOT NULL AUTO_INCREMENT,
        `user_id` INT NOT NULL,
        `area_id` INT NOT NULL,
        `required_mission` INT NULL,
        `completed_mission` INT NULL,
        PRIMARY KEY (`id`),
        FOREIGN KEY (`user_id`) REFERENCES `user` (`id`) ON DELETE CASCADE,
        FOREIGN KEY (`area_id`) REFERENCES `area` (`id`) ON DELETE CASCADE
    );
    
    ```
    
    ![mission_tabel.PNG](mission_tabel.PNG)
    
2. 프로젝트 세팅 완료
    
    node.js와 express, nodemon까지 설치완료하고 레포지토리도 생성하였다.
    
    레포지토리 주소: https://github.com/codie0226/UMC8Practice/tree/feature/chapter04
    
    ![기초 세팅 완료.PNG](기초세팅완료.png)
    
    ![실행겨로가.PNG](실행겨로가.png)
    

잘된다.