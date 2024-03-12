# สมาชิกกลุ่ม
1. 6410451393 นายวิทวัส พิณรัตน์ หา Dataset เก็บข้อมูลเพิ่มเติมเเละลองทดลองเทคนิคต่างในการจัดการกับ data ก่อนที่จะส่งไปเทรนภายในตัวโมเดลเช่นการทำ augmentation หรือปรับเเสดงเพื่อเพิ่มความเข้มของตัวอักษรซึ่งวิธีการเพิ่มลดความเข้มของตัวอักษรนั้นไม่เหมาะสม

2. 6410450842 นายชวิศ สิทธิธรรมจักษ์ ออกเเบบเเละเลือกใช้เทคนิคที่จะช่วยให้โมเดลใช้งานได้ดียิ่งขึ้น เช่นการเลือกใช้ VGG ซึ่งเป็น 1 ในรูปเเบบการออกเเบบ CNN กำหนดจำนวน layers เเละจำนวน node ในเเต่ละ layers เเละปรับเเต่งโมเดลให้มีประสิทธิภาพมากยิ่งขึ้นโดยการทำ regularize โดยการ dropout

# Preparing data
original alphabet written dataset : https://www.kaggle.com/datasets/dhruvildave/english-handwritten-characters-dataset/data

- ดาวน์โหลด dataset แล้ว unzip โฟลเดอร์หลังจาหนั้นให้เปลี่ยนชื่อโฟลเดอร์จาก 'archive' เป็น 'alphabets' แล้วนำโฟลเดอร์นี้ไปใส่ใน working ในโฟลเดอร์ alphabets ประกอบด้วย โฟลเดอร์ Img ที่เก็บรูปภาพและมีไฟล์ english.csv ที่เก็บ path ของชื่อรูปที่ตรงกับ label

- นำข้อมูลที่เก็บมาใส่ในโฟลเดอร์ Img และเพิ่มข้อมูลใน english.csv

# Preprocessing data

1. โหลด english.csv เข้ามาเป็น pandas dataframe
2. สร้างคอมลัมน์ใหม่ใน dataframe ชื่อ img โดยจะข้อมูลของรูป
3. นำเข้ารูปแล้วใส่ในคอลัมน์ img โดยปรับขนาดรูปเป็น 64 x 64
4. นำชื่อ class ทั้งหมดใส่ในตัวแปร class_names
5. ทำการแบ่ง train_test_split ของที่ละ class เป็น x_train, y_train, x_test, y_test (ข้อมูลจะยังเรียงจาก class 0-9A-Za-z)
6. ทำการสุ่มลำดับของข้อมูล
7. ทำ one-hot-encode กับ y_train, y_test

# creating model



# training model

