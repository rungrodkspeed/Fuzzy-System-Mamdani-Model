# การควบคุมเครื่องกรอกอากาศแบบอัตโนมัติโดยใช้เซตฟัซซีจากโมเดล Mamdani
### System
-------------
โดยเครื่องกรอกอากาศมี input อยู่ 2 อย่าง คือ ความเร็วของตัวดูดอากาศและ ความเร็วของปั้มน้ำที่ดึงออก
ซึ่งจะมี output เป็น ความเร็วของใบพัดที่นำอากาศที่กรอกเสร็จแล้วออกจากเครื่อง

### Rules
-------------
ในการออกแบบกฎของระบบนั้น เราจะออกแบบดังนี้
<p align="center">
  <img src="/blob/rules.PNG" />
</p>

### Membership function
-------------
โดยระบบนี้เราจะใช้ ฟังก์ชันสามเหลี่ยมเป็นฟังก์ชันความเป็นสมาชิกของค่า input ที่เข้ามาในระบบ
ซึ่งเราจะออกแบบ membership function ดังนี้

- vaccum velocity membership function
<p align="center">
  <img src="/blob/vv.PNG" />
</p>

- pump propeller velocity membership function
<p align="center">
  <img src="/blob/pv.PNG" />
</p>

- fan velocity (output) membership function
<p align="center">
  <img src="/blob/fv.PNG" />
</p>

### Fuzzification
-------------
ในการหาเหตุผล จะเริ่มจากการหาระดับความเข้ากันได้ของแต่ละอินพุตกับพจน์ภาษา ดังนั้นค่าความเป็นสมาชิกของแต่ละอินพุตในแต่ละพจน์ภาษาจะถูกรวมกันในลักษณ์ของตัวเชื่อม conjunction
พูดให้เข้าใจง่ายก็คือ การเปลี่ยนค่า input ให้อยู่ในรูปของฟัซซีเซต ในแบบของ Mamdani
ตามกฎที่เราตั้งเอาไว้ 
กำหนดให้ input คือ
- vaccum velocity 35 m/s
- pump propeller velocity 50 ml/s

จากนั้นเปลี่ยนค่าดังกล่าวให้อยู่ในรูปของค่าความเป็นสมาชิก เมื่อเปลี่ยนเสร็จแล้วจะได้ดังนี้
- vaccum velocity (membership) = [0.  , 0.5 , 0.25, 0.  , 0.  ]
- pump propeeler velocity (membership) = [0. , 0., 0. , 0.5, 0.16666667]

จากนั้นนำค่าดังกล่าวไปคำนวณหาค่า membership ของเอ้าท์พุต (fan velocity)

### Output system (Fuzzy set)
-------------
เมื่อคำนวณเสร็จแล้วจะได้ output ออกมาดังรูป
<p align="center">
  <img src="/blob/output.PNG" />
</p>

แต่ค่าที่ได้มานั้นยังอยู่ในรูปของ membership ดังนั้นเราจะต้อง defuzzification เพื่อให้เอ้าท์พุตอยู่รูปของช่วงตัวเลขที่สามารถควบคุมระบบได้

### Defuzzification
-------------
โดยกระบวนการที่เราจะ defuzzification นั้นเราจะใช้วิธีการแปลงโดยใช้ centroid  ซึ่งวิธีการดังกล่าวจะใช้ mode ของกราฟที่ผ่านการใช้ alpha cut แล้วหาจุดกึ่งกลางของกราฟที่ได้ดังภาพ

<p align="center">
  <img src="/blob/centroid.jpeg" />
</p>

จะได้ค่าเท่ากับ 58.31666666666666 m/s ซึ่งเป็นความเร็วของใบพัดที่นำอากาศที่ผ่านการกรองแล้วออกจากเครื่อง
