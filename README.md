import cv2
import mediapipe as mp
import time
from directkeys import right pressed , left pressed , up pressed , down pressed
from directkeys import PressKey , ReleaseKey
brake key pressed=left pressed
accelerate key
pressed=right pressed
jump key pressed=up pressed
slide key
pressed=down pressed
time . sleep (2.0)
current key
pressed = set ()
a variable
mp draw=mp. solutions . drawing
mp hand=mp. solutions . hands
tipIds =[4 ,8 ,12 ,16 ,20]
 video=cv2 . VideoCapture (0)
default camera
# suspends execution for a no. of sec
# build an unordered collection of unique elements assigns to
utils
# solution for drawing utils as we are drawing utils
# solution for hand pose
# List of landmarks of tip of fingers
# Start capturing video from webcam, 0 refers to computer or
### Hands fuction of mp processes RBG image amd returns hand landmarks and handedness of detected
hand
with mp hand.Hands(max num hands=1,min detection confidence =0.5 ,
hands to be detected at a time
min tracking confidence =0.5) as hands :
# max num hands = no. of
# min detection confidence
= min confidence value for detected person−model to be considered as successful .
while True :
# min tracking confidence =
min confidence value with which the detection from the landmark−tracking model must be
considered as successful
keyPressed = False
brake pressed=False
a ccelerator pressed=False
j ump pressed=False
s l i de pressed=False
key count=0
key pressed=0
r et , image=video . read ()
whether camera is working(1) or not (0)
image=cv2 . cvtColor (image , cv2 .COLOR BGR2RGB )
gives us BGR image
#image = cv2. cvtColor (src , cv2.COLORBGR2GRAY )
image . flags . writeable=False
model or image as not writtable
# Read video frame by frame & ret checks
# Convert BGR image to RGB image as opencv
# To improve the process performance we make
r e sults=hands . process (image)
# Process the RGB image only
image . flags . writeable=True
model or image as writtable
image=cv2 . cvtColor (image , cv2 .COLOR RGB2BGR )
l mList =[]
# As completed or trained the model make
# Convert RGB image to BGR image
# Empty list to store landmarks
### Prediction made by the model is saved in the results variable from which can access
l andmarks using results . multi hand landmarks
i f results . multi hand landmarks :
# If hands are present in image(frame)
f or hand landmark in results . multi hand landmarks :
variable results
myHands=results . multi hand landmarks [0]
of hand landmark i .e. 0
f or id , lm in enumerate(myHands. landmark) :
# Iterate all landmarks in
# provides starting point
# Enumerate through all ids
and landmarks to provide x,y,z coordinates of each landmark on image
h ,w, c=image . shape
assigns to h and w
cx , cy= int (lm.x*w) , int (lm.y*h)
# finds height and width of the image and
# finds actual integer coordinates of
l andmarks and store them in cx and cy
l mList . append ([ id , cx , cy ])
# Stores each landmark values and its
corresponding coordinates in an empty list one by one
mp draw. draw landmarks(image , hand landmark , mp hand.HAND CONNECTIONS) #
draw landmarks function is used to draw hand landmarks and connections on image
f i ngers =[]
cam at a time
i f len ( lmList ) !=0:
# list to count no. of fingers visible to
### This if statements used to check whether thumb is opened or closed
i f lmList [ tipIds [0]][1] > lmList [ tipIds [0] −1][1]:
# Checks if landmark if tip
of finger is less than a certain landmark on finger along Y−axis
f i ngers . append (1)
opened
else :
f i ngers . append (0)
# 1 is added to fingers list if thumb is
### This for loop block is used to check if other 4 fingers are opened or closed
f or id in range(1 ,5) :
i f lmList [ tipIds [ id ]][2] < lmList [ tipIds [ id ] −2][2]:
f i ngers . append (1)
# Corresponding no. of 1’s are added to
f i ngers list for no. of fingers opened
else :
f i ngers . append (0)
t o t al =fingers . count (1)
assigns count value to variable total
#
