#include "highgui.h"
#include "cv.h"

int main(void)
{
double wsize = 320;
double hsize = 240;

cvNamedWindow("FaceDetection", CV_WINDOW_AUTOSIZE);

CvCapture* capture = NULL;

capture = cvCreateCameraCapture(0);
cvSetCaptureProperty (capture, CV_CAP_PROP_FRAME_WIDTH, wsize);
cvSetCaptureProperty (capture, CV_CAP_PROP_FRAME_HEIGHT, hsize);

IplImage* frame;
CvHaarClassifierCascade* cvHCC = (CvHaarClassifierCascade*)cvLoad("/usr/share/o$
CvMemStorage* cvMStr = cvCreateMemStorage(0);
CvSeq* face;

while(1)
{
frame = cvQueryFrame(capture);
if(!frame) break;

face = cvHaarDetectObjects(frame, cvHCC, cvMStr);

for(int i=0; i < face->total; i++)
{
CvRect* faceRect = (CvRect*)cvGetSeqElem(face,i);
cvRectangle(frame, cvPoint(faceRect->x, faceRect->y), cvPoint(faceRect->x + fac$
}

cvShowImage("FaceDetection", frame);

if(cvWaitKey(30) == 27) break;
}

cvReleaseMemStorage(&cvMStr);
cvReleaseHaarClassifierCascade(&cvHCC);
cvReleaseCapture(&capture);

cvDestroyWindow("FaceDetection");
}

