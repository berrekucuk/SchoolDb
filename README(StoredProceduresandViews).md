# SchoolDb
## AddSchoolStaffs Prosedürü
```
CREATE PROCEDURE [dbo].[AddSchoolStaffs]
	@IdentityNumber INT,
	@Name VARCHAR(50),
	@PhoneNumber VARCHAR(11),
	@Email VARCHAR(50),
	@Position VARCHAR(50),
	@Branch VARCHAR(50),
	@DateofStart Datetime,
	@IsActive Bit,
	@CreatedDate Datetime,
	@UpdatedDate Datetime
AS
BEGIN
	INSERT INTO SchoolStaffs VALUES (@IdentityNumber,@Name,@PhoneNumber,@Email,@Position,@Branch,@DateofStart,@IsActive,@CreatedDate,@UpdatedDate)
END
```
**Açıklama** : Bu prosedür, Okul personellerine ait bilgilerin pratik şekilde eklenmesi için tasarlanmış bir prosedürdür.

##  GetAttendanceByStudentId Prosedürü
```
CREATE PROCEDURE [dbo].[GetAttendanceByStudentId]
AS
BEGIN
	SELECT 
		Students.Name as 'Öğrenci Adı',
		Lessons.LessonName as 'Dersin Adı',
		Classes.ClassName as 'Sınıfın Adı',
		IsInClass as 'Yoklama'
		FROM Attendances
		LEFT JOIN Classes on Attendances.ClassId = Classes.Id
		LEFT JOIN Lessons on Attendances.LessonId = Lessons.Id
		LEFT JOIN Students on Attendances.StudentId = Students.Id
END
```
**Açıklama** : Bu prosedür, Classes,Lessons ve Students tablolarındaki bilgileri baz alarak öğrencilerin derslerdeki devam durumunu temsil etmek amacıyla tasarlanmıştır.

## GetStudentExams
```
CREATE PROCEDURE [dbo].[GetStudentExams]
AS
BEGIN
SELECT 
	Students.Name as 'Öğrenci Adı',
	Classes.ClassName as 'Sınıf Adı',
	Lessons.LessonName as 'Dersin Adı',
	Exams.ExamDate as 'Sınav Tarihi',
	Exams.ExamType as 'Sınav Türü',
	Exams.Note as 'Sınav Sonucu'
	 FROM Exams
		LEFT JOIN Classes on Exams.ClassId = Classes.Id
		LEFT JOIN Lessons on Exams.LessonId = Lessons.Id
		LEFT JOIN Students on Exams.StudentId = Students.Id
END
```
**Açıklama** : Bu prosedür, Classes, Lessons ve Students toblolarındaki bilgileri baz alarak öğrencilerin sınav bilgilerini ve sınav sonuçlarını öğrenmek için tasarlanmış bir prosedürdür.


## ExamResultView 
```
CREATE VIEW ExamResultView
AS
	SELECT 
	Students.Name as 'Öğrenci Adı',
	Classes.ClassName as 'Sınıf Adı',
	Lessons.LessonName as 'Dersin Adı',
	Exams.ExamDate as 'Sınav Tarihi',
	Exams.ExamType as 'Sınav Türü',
	Exams.Note as 'Sınav Sonucu'
	 FROM Exams
		LEFT JOIN Classes on Exams.ClassId = Classes.Id
		LEFT JOIN Lessons on Exams.LessonId = Lessons.Id
		LEFT JOIN Students on Exams.StudentId = Students.Id
```
**Açıklama** : Öğrencilerin sınav bilgileri ve sınav sonuçlarının görüntülendiği tablodur.

## StudentAttendenceView
```
CREATE VIEW StudentAttendenceView
AS
	SELECT 
		Students.Name as 'Öğrenci Adı',
		Lessons.LessonName as 'Dersin Adı',
		Classes.ClassName as 'Sınıfın Adı',
		IsInClass as 'Yoklama'
		FROM Attendances
		LEFT JOIN Classes on Attendances.ClassId = Classes.Id
		LEFT JOIN Lessons on Attendances.LessonId = Lessons.Id
		LEFT JOIN Students on Attendances.StudentId = Students.Id
```
**Açıklama** : Bütün öğrencilerin yoklama bilgilerinin görüntülendiği tablodur.


