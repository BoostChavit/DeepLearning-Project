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

![alt text](<model_summary.png>)

สร้างโมเดลจาก CNN เเละ MLP โดย implement layers ของ CNN ตาม VGG Architectures เเต่ได้ทำการลดขนาดลงเพื่อลดระยะเวลาในการประมวลจากนั้นส่ง output ที่ได้ไปที่ fully connect NN 2 layers มีจำนวน NN layers 1024 node เเละมีจำนวน node ใน output layers ทั้งหมด 37 node ตามจำนวน class ที่ต้องการทำนาย


# training model

ทำการเเบ่งข้อมูลออกเป็น 2 ชุดโดยมีสัดส่วนคือ train 80% เเละ test 20% จากนั้นนำข้อมูลที่ได้ไปทำการทำ augmentation เพื่อเพิ่มประสิทธิภาพให้โมเดลก่อนที่จะส่งไปเทรนโมเดล


# ขั้นตอนการติดตั้งเเละทดสอบโมเดล
1. clone project จาก https://github.com/BoostChavit/DeepLearning-Project.git
2. ติดตั้ง library กรณีที่เครื่องผู้ใช้ยังไม่มี
    * cv2
    * pandas
    * numpy
    * keras, tensorflow
    * matplotlib
    * sklearn
3. ทดสอบลอง run program ที่ main.ipynb
4. หลังจากที่ทดสอบ run model ไปเเล้ว 1 ครั้งในกรณีที่ไม่มีอะไรผิดพลาดเเละไม่มี error จะได้ไฟล์ SSFF_model.h5 หากผู้ใช้ต้องการทดสอบโมเดลหรือนำโมเดลไปใช้สามารถใช้ผ่านโมเดล SSFF_model.h5 นี้ได้เลยโดยไม่ต้องเทรนใหม่อีกครั้งโดยมีนำโค๊ดด้านล่างไปใส่ไว้บรรทัดล่างสุดหลังจากการเทรนเเล้วสามารถใช้งานได้เลย
![alt text](<load_model.png>)