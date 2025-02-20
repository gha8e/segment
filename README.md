
# شرح عام للكود

هذا البرنامج يستخدم نموذج YOLOv8 Segmentation من مكتبة Ultralytics لاكتشاف الأجسام في الوقت الحقيقي عبر كاميرا الويب، ولكن بدلاً من وضع مربعات حول الأجسام، فإنه يقوم بتجزئتها ورسم حدودها بدقة. يتم التقاط كل إطار من الفيديو، تحليله باستخدام YOLO، وعرض النتائج مع الأجزاء المحددة للأجسام. يمكن للمستخدم إيقاف البرنامج بالضغط على "q".

# شرح الكود
import cv2 from ultralytics import YOLO 

استيراد مكتبة OpenCV لمعالجة الفيديو.

استيراد مكتبة Ultralytics YOLO لاستخدام نموذج YOLO للتجزئة.

model = YOLO("yolov8n-seg.pt") # تحميل النموذج 

تحميل نموذج YOLO للتجزئة (segmentation) (يجب التأكد من أن لديك ملف yolov8n-seg.pt).

cap = cv2.VideoCapture(0) 

فتح كاميرا الويب لالتقاط الفيديو.

while cap.isOpened(): success, frame = cap.read() 

بدء حلقة تكرارية لمعالجة كل إطار يتم التقاطه.

success يتحقق مما إذا تم التقاط الإطار بنجاح.

if success: results = model(frame) 

تمرير الإطار إلى نموذج YOLO لتحليل محتواه واكتشاف الأجسام وتجزئتها.

annotated_frame = results[0].plot() 

استخراج الإطار مع التوضيحات التي قام بها النموذج (مثل تمييز الأجزاء المجزأة للأجسام).

cv2.imshow("YOLO Inference", annotated_frame) 

عرض الإطار المعالج مع التوضيحات.

if cv2.waitKey(1) & 0xFF == ord("q"): break 

السماح للمستخدم بالخروج من البرنامج عند الضغط على "q".

else: break 

إذا فشل في التقاط الإطار، يتم إنهاء الحلقة.

cap.release() cv2.destroyAllWindows() 

