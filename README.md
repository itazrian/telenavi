# talenavi 090625 from Irvan T.

2. INFORMATION 
- Laravel Framework 8.83.29
- PHP 7.4.33 
- composer require maatwebsite/excel:^3.1 --with-all-dependencies

3. DATABASE
   
CREATE DATABASE `test_telenavi_090625` /*!40100 DEFAULT CHARACTER SET utf8mb3 */ /*!80016 DEFAULT ENCRYPTION='N' */;

USE `test_telenavi_090625`

CREATE TABLE todolists (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    assignee VARCHAR(255), -- optional
    due_date DATE NOT NULL,
    time_tracked DECIMAL(10,2) DEFAULT 0,
    status ENUM('pending', 'open', 'in_progress', 'completed') DEFAULT 'pending',
    priority ENUM('low', 'medium', 'high'),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

INSERT INTO test_telenavi_090625.todolists (title,assignee,due_date,time_tracked,status,priority,created_at,updated_at) VALUES
	 ('Learn Laravel','John Due','2025-06-13',0.00,'open','low','2025-06-09 14:41:58','2025-06-09 14:41:58'),
	 ('Learn Tailwind','John Due','2025-06-20',11.50,'pending','medium','2025-06-09 14:49:18','2025-06-09 14:49:18'),
	 ('Learn Postgree','John Due','2025-06-10',11.50,'completed','medium','2025-06-09 14:49:50','2025-06-09 14:49:50');

3. CURL API :  
 
3.1.API Create Todo List : 

curl --location 'http://127.0.0.1:8000/api/todolist' \
--header 'Content-Type: application/json' \
--data '{
    "title": "Learn Laravel",
    "assignee": "John Due",
    "due_date": "2025-06-13",
    "time_tracked": 0,
    "status": "open",
    "priority": "medium"
}'

3.2. API Get todo List to Generate Excel Report

curl --location 'http://127.0.0.1:8000/api/todolist/export?title=&assignee=John%20Due&start=2025-06-01&end=2025-06-30&min=0&max=1000&status=open%2Cpending%2Ccompleted&priority=low%2Chigh%2Cmedium'

3.3. API Get todo List to Provide Chart Data
curl --location 'http://127.0.0.1:8000/api/todolist/chart?type=status'
