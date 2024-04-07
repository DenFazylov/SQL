/*1.Создайте функцию, которая принимает кол-во сек и далее переводит их в кол-во дней, часов, минут, секунд.
Пример: 123456 ->'1 days 10 hours 17 minutes 36 seconds '*/
select
  CONCAT(
    FLOOR(123456 / 60 / 60 / 24),' days ',
    FLOOR(123456 / 60 / 60 - FLOOR(123456 / 60 / 60 / 24) * 24),' hours ',
    FLOOR(123456/60 - FLOOR(123456 / 60 / 60 / 24)*24*60 - FLOOR(123456 / 60 / 60 - FLOOR(123456 / 60 / 60 / 24) * 24)*60), ' minutes ',
    123456- 
    FLOOR(123456/60 - FLOOR(123456 / 60 / 60 / 24)*24*60 - FLOOR(123456 / 60 / 60 - FLOOR(123456 / 60 / 60 / 24) * 24)*60)*60 
    - FLOOR(123456 / 60 / 60 - FLOOR(123456 / 60 / 60 / 24) * 24)*60*60 
    -FLOOR(123456 / 60 / 60 / 24)*60*60*24, ' seconds'
  ) as this_time;


  /*2.Cоздайте процедуру, которая выведет только числа, делящиеся на 15 или 33 в промежутке от 1 до 1000.
Пример: 15,30,33,45...*/


DELIMITER //
DROP PROCEDURE IF EXISTS while_cycle//
CREATE PROCEDURE while_cycle (IN num INT)
BEGIN
	DECLARE i INT DEFAULT 1;
    DECLARE x VARCHAR(50) default 0;
	IF (num > 0) THEN
		WHILE i < num DO
			IF (i % 15 = 0) and (i % 33 = 0) THEN
				SELECT i as 'Число, делящееся на 15 и 33';
			END IF;
			SET i = i + 1;
		END WHILE;
	ELSE
		SELECT 'Ошибочное значение параметра';
	END IF;
END//
DELIMITER ;

CALL while_cycle(1000);