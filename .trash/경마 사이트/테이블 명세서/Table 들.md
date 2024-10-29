### 1. 소유자 정보 (owner)

```sql
CREATE TABLE owner (
    owner_id INT PRIMARY KEY AUTO_INCREMENT,
    owner_name VARCHAR(255),
    english_owner_name VARCHAR(255),
    owner_number INT,
    address VARCHAR(255)
);
```

### 2. 조교사 정보 (trainer)

```sql
CREATE TABLE trainer (
    trainer_id INT PRIMARY KEY AUTO_INCREMENT,
    trainer_name VARCHAR(255),
    english_trainer_name VARCHAR(255),
    trainer_number INT,
    address VARCHAR(255)
);
```
### 3. 경주마 정보 (horse)
```sql
CREATE TABLE horse (
    horse_id INT PRIMARY KEY AUTO_INCREMENT,
    horse_name VARCHAR(255),
    english_horse_name VARCHAR(255),
    birth_date DATE,
    sex CHAR(1),
    color VARCHAR(50),
    age INT,
    nationality VARCHAR(100),
    import_country VARCHAR(100),
    breed VARCHAR(100),
    father_id INT,
    mother_id INT,
    grandfather_id INT,
    use_purpose VARCHAR(255),
    owner_id INT,
    trainer_id INT,
    stall_id INT,
    origin VARCHAR(255),
    rating INT,
    FOREIGN KEY (father_id) REFERENCES horse(horse_id),
    FOREIGN KEY (mother_id) REFERENCES horse(horse_id),
    FOREIGN KEY (grandfather_id) REFERENCES horse(horse_id),
    FOREIGN KEY (owner_id) REFERENCES owner(owner_id),
    FOREIGN KEY (trainer_id) REFERENCES trainer(trainer_id)
);
```


### 4. 기수 정보 (jockey)
```sql
CREATE TABLE jockey (
    jockey_id INT PRIMARY KEY AUTO_INCREMENT,
    jockey_name VARCHAR(255),
    english_jockey_name VARCHAR(255),
    jockey_number INT
);
```

### 5. 경주 정보 (race)

```sql
CREATE TABLE race (
    race_id INT PRIMARY KEY AUTO_INCREMENT,
    race_name VARCHAR(255),
    race_date DATE,
    race_day VARCHAR(50),
    race_distance INT,
    track_condition VARCHAR(50),
    weather VARCHAR(50),
    race_course VARCHAR(255),
    grade VARCHAR(50),
    prize_money1 INT,
    prize_money2 INT,
    prize_money3 INT,
    prize_money4 INT,
    prize_money5 INT
);
```

### 6. 경주 기록 (race_record)

```sql
CREATE TABLE race_record (
    race_record_id INT PRIMARY KEY AUTO_INCREMENT,
    race_id INT,
    horse_id INT,
    jockey_id INT,
    trainer_id INT,
    owner_id INT,
    position INT,
    time TIME,
    margin FLOAT,
    odds FLOAT,
    FOREIGN KEY (race_id) REFERENCES race(race_id),
    FOREIGN KEY (horse_id) REFERENCES horse(horse_id),
    FOREIGN KEY (jockey_id) REFERENCES jockey(jockey_id),
    FOREIGN KEY (trainer_id) REFERENCES trainer(trainer_id),
    FOREIGN KEY (owner_id) REFERENCES owner(owner_id)
);
```

### 7. 경주 세부 기록 (race_detail)

```sql
CREATE TABLE race_detail (
    race_detail_id INT PRIMARY KEY AUTO_INCREMENT,
    race_id INT,
    horse_id INT,
    section VARCHAR(50),
    time TIME,
    position INT,
    FOREIGN KEY (race_id) REFERENCES race(race_id),
    FOREIGN KEY (horse_id) REFERENCES horse(horse_id)
);
```
