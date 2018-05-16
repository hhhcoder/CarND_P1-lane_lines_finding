# **Finding Lane Lines on the Road**

## Writeup


### 1.Description of the pipeline
 
My pipeline consisted of 5 steps. 1.Convert to grayscale. 2.Gaussian blur.3.Canny edge detection. 4.Hough lines.
Thanks for the helper functions! Before used them, I have read and tested them all. But there is a question confuse me, in the "draw_lines" function, these codes seems no effect.

left_center_mean=left_center_mean[0]+left_len[i]*left_center[i][0],left_center_mean[1]+left_len[i]*left_center[i][1]#is it useful?left_slope_mean+=left_slope[i]*left_len[i]#is it useful?
right_center_mean=right_center_mean[0]+right_len[i]*right_center[i][0],right_center_mean[1]+right_len[i]*right_center[i][1]#is it useful?
right_slope_mean+=right_slope[i]*right_len[i]#is it useful?


  By theses helper functions and default parameters, images, "solidWhiteRight.mp4" and "solidLeftYellow.mp4" are already work, but in the test of "challenge.mp4", it looks failed. In this video, there are too many disturbance. So I decide to change the default parameters to make it work.
  At first, in this scenario, the car drives on a curve road, so I change the interest region and "draw_lines" function.
In contrast to the default parameter of interest region "imshape[0]*0.6", 0.65 seems better.
(After some times trail, some error about the process "ffmpeg-win32-v3.2.4.exe" will happened, could you tell me why and how to prevent it?)
  The effect seems better, but it untill not good, especially go through the shadow of the tree.
  So I concide restart to confirm the mask region through the clip image of video and increase the "kernel_size" of gaussian blur.
  Finally, I changed the mask region with to quadrangle of "vertics1" and "vertics2". And increase the kernel size from 5 to 7, so that obtain a better output. I think it could be better if I shrink the interest region and increase the gaussian, but the error of "'NoneType' object is not iterable" really trouble me. So I stop at this step because the limited time, so sorry.

vertics1=np.array([[(0,imshape[0]),(imshape[1]/2-20, imshape[0]*0.65), (imshape[1]/2+20, imshape[0]*0.65), (imshape[1], imshape[0])]], dtype=np.int32)
vertics2=np.array([[(imshape[1]/2-140,imshape[0]),(imshape[1]/2+25, imshape[0]*0.72), (imshape[1]/2+25, imshape[0]*0.72), (imshape[1]/2+240, imshape[0])]], dtype=np.int32)

                

