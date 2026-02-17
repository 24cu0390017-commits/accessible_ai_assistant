import cv2
import mediapipe as mp

mp_hands = mp.solutions.hands
hands = mp_hands.Hands()
mp_draw = mp.solutions.drawing_utils

cap = cv2.VideoCapture(0)

while True:
    success, img = cap.read()
    imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    results = hands.process(imgRGB)

    if results.multi_hand_landmarks:
        for handLms in results.multi_hand_landmarks:
            mp_draw.draw_landmarks(img, handLms, mp_hands.HAND_CONNECTIONS)

            fingers = 0
            tips = [4, 8, 12, 16, 20]

            for tip in tips:
                if handLms.landmark[tip].y < handLms.landmark[tip - 2].y:
                    fingers += 1

            if fingers == 1:
                print("FORWARD")
            elif fingers == 2:
                print("LEFT")
            elif fingers == 3:
                print("RIGHT")
            elif fingers == 5:
                print("STOP")
            else:
                print("EMERGENCY")

    cv2.imshow("Gesture Based AI System", img)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
