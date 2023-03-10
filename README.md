# MyOpenCV

1.gray webcam
실행 하기 전 웹캠과 연결하고 실행 하면 웹캠에 보이는 화면이 회색으로 출력이 됩니다.
<pre>
<code>
import cv2
import numpy as np

def sketch(image):
    img_gray = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)                   #이미지를 회색 이미지로 변환
    img_gray_blur = cv2.GaussianBlur(img_gray,(5,5),0)                  #회색이미지에 Gaussion Blur 적용
    canny_edges = cv2.Canny(img_gray_blur,10,70)                        #가우시안 이미지에 캐니 에지 감지 적용
    ret,mask = cv2.threshold(canny_edges, 70,255,cv2.THRESH_BINARY_INV) #이미지 반전하고 이진 반전 이미지를 얻는다.
    return mask

cap = cv2.VideoCapture(0)         #웹캡에 접근
while True:
    ret,frame = cap.read()
    cv2.imshow("Our Live Sketcher", sketch(frame))
    if cv2.waitKey(1) == 27:      #esc키로 종료
        break
cap.release()
cv2.destroyAllWindows()
</code>
</pre>
![image](https://user-images.githubusercontent.com/50050003/224374627-b0cb91a8-16c9-40cc-acc4-d30fbf4418a5.png)
인식이 잘 확인이 되도록, 눈을 크게 이를 보이게, 옷을 셔츠 무의 옷을 입어 촬영하였습니다.
