# How to best implement your video capture setup
Comprehensive method for selecting the right video acquisition equipment for your experimental setup

... work in progress ...
<p align="justify">
Below we outline some concepts that are critical for successful implementation of digital video recording.
The quality of video data, and therefore the results obtained from it, depends heavily on experimental conditions such as lighting, camera position, camera resolution, optical quality, background color, etc. The influence of these parameters on behavioral results has rarely been studied, and most researchers are unfamiliar with the variables to be taken into account and how to adjust them. It is also important to note that parameters such as resolution, frame rate, or encoding configuration can have an exponential impact on the computational cost of processing algorithms. 
Below we outline some concepts that are critical for successful implementation of digital video recording.
</p>
## Choose the right tool
<p align="justify">
There are countless relevant video capture solutions available, of all qualities and at all prices, whether it be a consumer camera, security camera, action cam (such as a GoPro), or electronic device embeded camera (such as a Raspberry Pi). Each of these solutions has its pro and cons.
In the context of experimental laboratory systems, it is more convenient to use a camera connected to a computer, which will facilitate control, synchronization, and data storage. Modern industry USB cameras can be very good options for laboratories that are well versed in prototyping, programming, and software control layers. 
</p>
Above all, in order to choose the right video acquisition system, it is necessary to define the experimental conditions:
1. maximum width of the field of view
2. maximum distance at which the camera can be positioned (space constraints)
3. spatial resolution, the accuracy required for the analysis (For behavior, we generally use 1mm or less)
4. speed of the action to be recorded (open field : 8cm/s = 30fps, treadmil :  up to 150cm/s = 200fps)
5. light intensity and quality (<100lux = low, infrared)

- 1 and 3 allow you to calculate the pixel resolution needed : ie: arena width = 25cm, resolution = 1mm/pix --> 250 pixels. Following Nyquist's theorem, we can double this number of pixels : 500pix is the higher width of the sensor
- 4 and 5 guide the choice of sensor characteristics: larger pixel size for greater sensitivity, high-performance signal-to-noise ratio management, infrared filter or not, framerate
- 4 and sensor resolution are decisive in choosing the connection type: ie: USB3 camera can transfer images of 1900x1200 at 150fps (only Camera Link will allow high throughput for large images at a high frame rate.)
- 2 and sensor size and resolution are necessary to choose the right lens

 ![Capture_basler_lens](https://github.com/user-attachments/assets/194a9b7e-c5da-4856-b350-2aa03a5aae0e)
(Lens Selector Basler AG : https://www.baslerweb.com/fr-fr/tools/lens-selector/)

## Camera Configuration Guidelines
<p align="justify">
To obtain biometric behavioral data, digital video files have to be initially recorded. Digital video is spatial and temporal sampled frames presented in a sequence. The spatio-temporal sampling unit which is usually called pixel (picture element) can be represented by a digital value to describe its color and brightness. 
A good quality video is made up of images that are large enough to be clearly legible, sufficiently resolved to be precise, and sharp in both still and moving areas, with good contrast, while remaining rich in information. In other words, we need sufficient definition so that objects are made up of enough pixels to be well detected, good resolution so that we can distinguish the various elements making up the image, focus so as to avoid blurring in the area observed, and an exposure time adapted to the speed of movement likely to be recorded to avoid motion blur. It's also important to maintain a high dynamic range so that subtle textures and variations are preserved. Finally, we need to pay particular attention to the method used to encode the video file, and especially to the compression mode applied to reduce file size during storage.
The video acquisition system can be divided into four parts:
	- the camera (sensor + electronics)
	- the optical system that projects the image onto the sensor
	- the lighting
	- the software that controls the camera and encodes the video file
</p>
### Connectivity
<p align="justify">
The connectivity of a camera is often a crucial issue, the answer to which will determine the choice of cameras with which to equip the setup.
– USB 2.0: this inexpensive system requires a cable connection to the camera (up to 5 metres long). With a theoretical data transfer rate of up to 480 Mbits/s, this system can nevertheless be unreliable in terms of data transmission. It has now been superseded by USB 3.0.
– USB 3.0: this interface has similar characteristics to USB 2.0, but offers better throughput and more reliable transmission. (The maximum length of a USB cable is 5 meters. However, it is possible to exceed this limit by using a repeater, which can add an additional 5 meters.)
– CameraLink: with very high throughput (up to 6 Gbit/s), this very expensive communication interface is perfect for high resolutions. The cable length can be up to 10 metres.
– GigE (or Giga Ethernet): with a data transfer rate of up to 1 Gbit/s, this very inexpensive communication interface is advantageous if you need long cable lengths (up to 100 metres).
– PoE (or Power Over Ethernet): its speed can reach up to 1 Gbit/s, and its main advantage is that it can power the camera at the same time as data communication takes place
</p>
### Sensor resolution and Optics Choice
<p align="justify">
In order to choose the right camera from the plethora of options on the market, you need to ask yourself the right questions:
- How big is my experimental setup: how wide is the field I want to record?
- How far away can I set up the camera (space constraints, available space)?
- What's the max speed of the movements/behaviors I want to analyze?
- What lighting conditions do I need for my experiment?

The optical component plays the most important role in image quality and determines whether the entire scene can be captured. However, it cannot be chosen without taking into account the specific characteristics of the camera sensor (size, resolution, sensitivity).So that's where we'll start.
</p>
#### Image size: sensor size and resolution
<p align="justify">
One might think that simply choosing the sensor with the most pixels would guarantee the best image quality, but the technical reality is not that simple.
The sensor is an electronic component made of silicon, copper and glass that collects light from the lens and converts it into electrical information. In the image production chain, it is then up to the image processing processor to convert this analogue signal into digital information (using 0 and 1). To collect light, the sensor is divided into multiple small light wells, called photosites, which are usually square and whose size is expressed in microns (µm) or even nanometres (nm). The information from each individual photosite becomes, after passing through the processor, a pixel (picture element) that makes up the image. 

Depth of field is greater on a small sensor, which is an advantage in video. A smaller sensor allows for smaller cameras that are easier to stabilize and generate less heat. Due to their physical properties, these sensors also transmit electrical signals more quickly, resulting in higher video frame rates. A small sensor therefore seems to be a reasonable choice, but in order for objects of interest to be correctly identified in the image, they must be made up of enough pixels, and for this, the number of pixels in the camera sensor must be taken into account. 

The larger the sensor, the larger the photosites (at equal pixel density), which allows for higher sensitivity. The disadvantage of a larger sensor is that the lens will also have to be larger, and therefore heavier and more expensive. It also has a shorter depth of field, i.e. a reduced area of sharpness in the depth of the scene. Furthermore, the electrical signal takes longer to travel from one end to the other, which limits refresh rates and makes the highest photo and video frame rates less accessible.

It's important to understand that each digital video file is characterized by a specific resolution. This corresponds to the number of pixels used to define an area in the actual scene, and depends on the total number of pixels in the camera sensor. Most modern digital cameras can record in high‐definition (HD; 1920 × 1080 pixels) or even ultrahigh‐definition (UHD; 3840 × 2160 pixels) resolution. 
Pixel density is determined by the number of photosites per unit area and ensures that objects in the image can be clearly distinguished. To achieve this, the lens associated with the sensor must be carefully chosen and its characteristics must correspond to both the size and number of pixels in the sensor.
</p>
#### Lens
<p align="justify">
When choosing a lens for your camera, it is essential to ensure that the optic is adapted to size of your sensor and that the resolution of the lens is compatible with the pixel size of the sensor. (Lens resolution is measured in line pairs per millimeter (lp/mm), which directly affects overall performance and image quality. Some guides are available to give lens resolution in line pairs per millimeter, and explain how to calculate their compatibility with your camera for optimum results but the sheer number of camera references and the diversity of sensor sizes, resolutions and sensitivities, as well as the constant evolution of technologies, make any attempt to describe the various combinations tedious and pointless. Serious manufacturers offer a configurator application which, based on the characteristics of your experimental set-up, allows you to define the characteristics of your acquisition system.
</p>p>
![focal objectifvsCapteur](https://github.com/user-attachments/assets/a6c40451-a955-448d-9faf-0e0b4e3409e4)
https://www.edmundoptics.fr/knowledge-center/application-notes/imaging/how-to-choose-a-variable-magnification-lens/

#### Frame Rate and Exposure Time Trade‑offs
<p align="justify">
A very important part of the acquisition system that should guide your choice is the ability to customize essential settings such as exposure time and frame rate. To correctly describe behavior or movement, we need to acquire images at an appropriate sampling rate, known as frame rate. This parameter denotes the number of still frames acquired per second. Hence, it is often referred to in the camera settings as the frames per second (fps) parameter. A video comprising a frame rate of thirty frames per second looks fairly smooth enough for most purposes. 
Another critical parameter for quality acquisition is exposure time, which determines image sharpness and the amount of light reaching the sensor. This corresponds to the shutter speed of the camera. It is this parameter, adapted to the maximum speed of the events observed, that will allow the animal to remain in focus and its behavior identifiable regardless of its attitude.
The parameters of frame rate and exposure time are therefore interdependent: frame rate defines the level of motion sampling, exposure time defines motion sharpness. It's easy to understand that the accurate description of fast motion will require many frames per second and a short exposure time. Lighting must therefore be adapted accordingly to obtain sufficiently bright images. We therefore have three key parameters: frame rate, exposure time and amount of light, for which we need to find the best compromise.

In specific circumstances both frames per second and shutter speed parameters might also need to be empirically optimized. This is particularly pertinent when using illumination sources that appear to “flicker” on the camera screen. “Flickering” occurs when the recording frame rate is higher than the cycle of electricity through the lighting circuit. The grid electricity operates on alternating current with a particular frequency such as 50 Hz (60 Hz in the United States), which means the circuit is turning on/off 100 (120 in the United States) times per second. Although not visible to the naked eye, that flicker can be seen through a camera lens when the shutter settings are not in sync with the hertz value of the main electricity that powers the illumination sources. To avoid such flicker, one can reduce the recording frame rate and adjust the shutter speed to closely match it to the hertz frequency (for 50‐ and 60‐Hz grids a shutter speed divisible by 50 and 60, respectively). Some power supply drivers specifically designed for videography applications rectify the main current from 50 or 60 to 120 Hz, thus completely eliminating the issue. In general, battery‐operated or direct‐current lights are not plagued by such problems. However the implementation of a pulse width modulation, or dimmer, which operates at a low frequency in the direct‐current lighting circuit, can induce identical effects (light‐emitting diode -LED- lights with low‐frequency pulse width modulation controllers are used to adjust the intensity of light)

To maintain a clear image even with a low exposure time, the size of the sensor's photosites and its ability to increase ISO (sensitivity to noise generated by increased gain) must be taken into account. Gain is a parameter that must also be accessible if the amount of light cannot be increased, but increasing the gain requires high-quality electronics to avoid generating counterproductive noise on the sensor.
</p>
#### Lighting
<p align="justify">
Scene lighting is an important factor in video quality. It is usually limited so as not to disturb the animal in its task and not to influence its behaviour. It may be advisable to use infrared lighting, which does not disturb the animal. Monochrome cameras generally do not have IR filters, which allows videos to be captured without modification. For colour cameras, an IR filter allows for purer colours, and depending on the camera model, it is sometimes possible to remove it quite easily (however, be aware that this may alter the colour rendering in the camera's colour mode). We recommend using filters and corresponding IR illumination sources with a wavelength of light of approximately 850 nm. These wavelengths are advantageous because they allow for illumination of organisms in complete darkness. Furthermore, most animals are incapable of seeing this spectrum of light. https://pmc.ncbi.nlm.nih.gov/articles/PMC9826254/pdf/ETC-41-2342.pdf
Some recommendations to avoid analysis difficulties:
- Check that the lighting is uniform across the device (prefer indirect lighting, avoid shadows and overexposed or flickering areas).
- Avoid reflections by using matte or anti-reflective materials, possibly using a polarising filter on the camera lens.
</p>
### Compression Strategies
#### codec
<p align="justify">
The last point concerning the quality of the video file is the recording format. This is an often overlooked but critically important factor, whether for file playback, file size, or, most importantly, the quality of the recorded information. Because raw high-resolution video sequences consume large amounts of digital storage, data are often compressed using a range of available compression and decompression algorithms: “codecs.” Examples include H.264, MPEG, and ProRes. Based on selecting different camera settings, the compression can be performed to different standards that include selection of codecs as well as file digital containers (the “format” AVI, MP4, MKV, MOV...), which is how the file will be “packaged” with certain metadata and can be identified by different software. Video compression reduces file size by removing redundant information and using lossy techniques to approximate the original content. Compression algorithms often smooth out details, which can obscure small movements. Artifacts introduced by compression can also mislead tracking algorithms, resulting in inaccuracies
The early form of video compression was described as the difficulty of transmitting successive images of video can be avoided by only sending the difference between the successive images, though it was not actually used, however, it became the foundation for the video compression standards today. Video signals are constructed by a sequence of still images which are better known as video frames. These frames can be encoded for compression using intra frame coding techniques but this compression does not turn out to be of enough good value for a video. This fact and presence of temporal redundancy inside the video sequence drives the need of inter frame encoding. A prediction of actual video frame based on previous frame is subtracted from actual frame to form what is called residual frame. The residual frame is then encoded by frame codec.

Zhang et al. explained the concept of typical video compression nowadays as following :  The video compression consists of the encoder compressing the images into the compressed form, which can be stored or transmitted to another location, and the decoder to decompress the images. This process of coding and decoding is also called a codec. There are two types of video coding: lossless coding and lossy coding. Lossless coding compresses the images and obtains the reconstructed images after decompression without any loss of information. Lossy coding, however, compresses the images by removing the less important information, which will sacrifice the image quality to the level the human visual system can tolerate. Lossy compression is more widely used today since it allows a much smaller compressed size and is more efficient than the lossless compression. Various video compression standards have been developed, such as MPEG and H.26X series. H.264/AVC is the most widely used standard nowadays and supports up to 4k resolution of video. H.265, so-called High Efficiency Video Coding (HEVC), was developed based on H.264/AVC structure and is a more recent standard that has been released in 2013. H.265/HEVC supports up to 8k resolution of the video
</p>
#### Key Frames and Compression:
<p align="justify">
 Key Frames (I-Frames) are complete images stored periodically in the video. Between key frames, only the differences from the previous frames (P-frames and B-frames) are stored. If key frames are infrequent, the quality and detail of intermediate frames can degrade, making it harder to detect subtle movements accurately. This is because P-frames and B-frames rely on predictive coding, which can introduce artifacts, especially if the animal movements are small and slow.
To mitigate the impact of key frames and compression on detecting slow or small movements, you can consider the following approaches :
- Increase Key Frame Frequency: If you have control over the video recording settings, increase the frequency of key frames. This ensures that there are more complete images, reducing the reliance on predictive frames.
</p>
## References
- Henry, J., & Bai, Y. (2022). Digital video recording in behavioral ecotoxicology. Environmental Toxicology and Chemistry, 41(9), 2342–2353. https://doi.org/10.1002/etc.5378
- Mathis, A., et al. (2018). DeepLabCut: markerless pose estimation of user-defined body parts with deep learning. Nature Neuroscience, 21(9), 1281–1289. https://doi.org/10.1038/s41593-018-0209-y
- Pereira, T. D., et al. (2022). SLEAP: Multi-animal pose tracking. Nature Methods, 19, 486–495. https://doi.org/10.1038/s41592-022-01426-1
- Zhang, X., et al. (2019). Video compression fundamentals. IEEE Transactions on Circuits and Systems for Video Technology, 29(1), 1–19.
- Bradski, G. (2000). The OpenCV Library. Dr. Dobb’s Journal of Software Tools.
