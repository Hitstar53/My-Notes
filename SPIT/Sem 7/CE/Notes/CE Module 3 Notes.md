### Module 3: Television Systems
#### 3.1: Introduction to PAL, NTSC, and SECAM TV Systems
Television systems vary across regions and were developed to cater to specific requirements for color encoding, resolution, and frame rates. The three primary global standards are **NTSC**, **PAL**, and **SECAM**, each with unique technical attributes and geographical distribution.

##### Scanning and Synchronization in TV
Television systems rely on **scanning** and **synchronization** to convert visual information into electrical signals and reproduce them accurately on the screen. This process ensures the faithful rendering of images and videos for viewers.

##### 1. Scanning in TV
Scanning is the process by which the optical image formed on a photosensitive plate of TV camera is broken into  many small picture elements called as pixels. Scanning refers to the systematic process of breaking an image into horizontal lines (raster) and converting them into electrical signals for transmission. These signals are then reconstructed into images at the receiver.
##### Types of Scanning
1. **Progressive Scanning (Direct Scanning)**:
    - Here, an electron beam scans the picture frame from left to right an goes from top to bottom until it reaches the extreme right at the bottom.
    - It offers smooth motion and higher picture quality, especially for fast-moving scenes.
    - This method is simple, but produces flickering
    - **Applications**: Used in modern digital TV systems, computer monitors, and gaming displays.
    - **Example**: HDTV resolutions such as 720p or 1080p.
      
2. **Interlaced Scanning**:
    - In interlaced scanning, each frame is divided into two fields:
        - **Odd lines** are scanned first (Field 1).
        - **Even lines** are scanned second (Field 2).
    - The two fields are interlaced to form a complete frame.
    - It reduces flicking
    - **Applications**: Traditional analog TV systems like PAL and NTSC.
    - **Example**: Standard Definition TV (SDTV) resolutions like 1080i.
##### Scanning Parameters
1. **Aspect Ratio**: Defines the width-to-height ratio of the image (e.g., 4:3 for SDTV, 16:9 for HDTV).
2. **Frame Rate**: Number of frames transmitted per second (e.g., 25 fps for PAL, 30 fps for NTSC).
3. **Resolution**: Number of horizontal lines and pixels per line (e.g., 625 lines for PAL).


##### 2. Synchronization in TV
It is the process by which the horizontal and vertical sweeps of the electron beam at both the camera (transmitter) and picture tube (receiver) are kept in step with each other. So separate synchronizing signals are transmitted along with the picture information. They are also called as tinting pulses and are rectangular in shape. Synchronization ensures that the scanning process at the transmitter and receiver occurs in perfect alignment, preventing distortion or loss of image clarity.
##### Types of Synchronization
1. **Horizontal Synchronization**:
    - Aligns the start and end of each horizontal line scan.
    - Uses **horizontal sync pulses** to reset the electron beam to the start of the next line.
2. **Vertical Synchronization**:
    - Ensures alignment of the vertical scanning process between transmitter and receiver.
    - Employs **vertical sync pulses** to reset the beam to the top of the screen after completing a frame.
3. **Color Synchronization**:
    - In color TV systems, a **color burst signal** synchronizes the color subcarrier frequency between transmitter and receiver.
    - This ensures proper decoding of color information (e.g., hue and saturation).
##### Synchronization Signals
- **Composite Signal**: Combines video signals with sync pulses.
    - **Structure**:
        1. Video Information (Luminance + Chrominance).
        2. Horizontal and Vertical Sync Pulses.
        3. Blanking Intervals.

##### 3. Signal Composition in TV Transmission
**Composite Video Signal**: A TV composite signal includes:
1. **Luminance Signal (Y)**: Represents brightness or intensity information.
2. **Chrominance Signal (C)**: Encodes color information.
3. **Synchronization Signals**:
    - Horizontal sync pulses.
    - Vertical sync pulses.

**Waveform**:
- The composite signal contains sync pulses and video signals arranged in a standard format to ensure proper decoding at the receiver.


##### NTSC (National Television Standards Committee)
The NTSC standard, established in the United States in 1954, was the first color television broadcast system. Designed to be backward-compatible with black-and-white TVs, it was a pioneering step in consumer electronics.

**Technical Parameters**:
- **Resolution**: Offers resolutions such as 720 × 480, 704 × 480, and lower variants (e.g., 352 × 240).
- **Frame Rate**: Operates at **29.97 Hz**, providing smoother motion for fast-moving scenes, which is advantageous for sports and live events.
- **Lines**: Utilizes **525 lines per frame** with interlaced scanning, where two fields combine to form a single frame.

**Color Encoding**:  
NTSC employs the **YIQ color model**, where:
- **Y** represents luminance (brightness).
- **I** and **Q** are the chrominance components, encoding hue and saturation.  

This encoding, however, is sensitive to phase errors, which can lead to hue distortions during transmission.

**The Countries that support NTSC video are as follows:** 
Antilles, Netherlands, Bahamas, Barbados, Belize, Bermuda, Bolivia, Burma, Canada, Chile, Columbia, Costa Rica, Cuba, Dominican Republic, El Salvador, Ecuador, Grenada, Guatemala, Honduras, Jamaica, Japan, Mexico, Panama, Peru, Philippines, Puerto Rico, South Korea, Surinam, Taiwan, Tobago, Trinidad, United States of America, Venezuela.

**Advantages**:
1. Early adoption made it widely accepted in broadcasting.
2. Smoother motion due to a higher frame rate, reduces flicker.
3. Less inherent picture noise better S/N ratio.
4. Simpler circuits than PAL & SECAM, hence less costly than both.
5. Easy studio mixing.

**Disadvantages**:
1. Lower number of scan lines hence lower resolution compared to PAL and SECAM.
2. Susceptibility to hue fluctuation / color distortion due to phase errors.
3. Small luminance signal bandwidth (3.85 MHz), increased likelihood of interference.
4. Lower gamma ratio (2.2 as opposed to 2.8 in PAL systems).
5. More costly than SECAM.

##### PAL (Phase Alternating Line)
PAL was introduced in 1967 by the UK and Germany to address the color reproduction challenges of NTSC. Its design prioritized better picture quality and resilience to transmission errors.

**Technical Parameters**:
- **Resolution**: Standard resolutions include **720 × 576** and lower variants (e.g., 352 × 288).
- **Frame Rate**: Operates at **25 Hz**, synchronized with the European mains frequency of 50 Hz.
- **Lines**: Employs **625 lines per frame**, offering higher resolution than NTSC.

**Color Encoding**:  
PAL utilizes the **YUV color model**:
- **Y**: Luminance.
- **U, V**: Chrominance (color information).  
    The system alternates the phase of the chrominance signal line-by-line, effectively canceling out phase errors and ensuring accurate color reproduction.

**The countries that support PAL are as follows:** 
Algeria, Andorra, Angola, Argentina, Australia, Austria, Bahrain, Bangladesh, Belgium, Botswana, Brazil, Brunei, Cameroon, China, Denmark, Ethiopia, Fiji, Finland, Germany, Ghana, Gibraltar, Hong Kong, Iceland, India, Indonesia, Ireland, Israel, Italy, Jordan, Kenya, Kuwait, Lesotho, Liberia, Luxemburg, Malawi, Malaysia, Maldives, Malta, Mozambique, Namibia, Netherlands, New Zealand, Nigeria, Norway, Oman, Pakistan, Papua New Guinea, Paraguay, Portugal, Qatar, Rumania, Seychelles, Sierra Leone, Singapore, Somalia, South Africa, Spain, Sri Lanka, Sudan, Swaziland, Sweden, Switzerland, Syria, Tanzania, Thailand, Turkey, Uganda, United Arab Emirates, United Kingdom, Uruguay, Yemen, Yugoslavia, Zambia, Zimbabwe.

**Advantages**:
1. Greater Number of Scan lines, therefore more picture detail.
2. Wider Luminance Signal Bandwidth (4.43 MHz in most)
3. Higher resolution provides sharper images.
4. Higher Gamma Ratio (2:8) hence higher level of Contrast than NTSC.
5. Stables Hues due to error correction by phase alternation, which minimizes color distortion.
6. Easy studio mixing compared to SECAM.

**Disadvantages**:
1. Lower S/N Ratio than NTSC.
2. Lower frame rate, hence more flicker.
3. Costliest receivers due to complex circuits for electronic switching.


##### SECAM (Séquentiel Couleur Avec Mémoire)
SECAM, developed in France in 1967, prioritized robustness over picture quality. Its design makes it highly resilient to signal degradation over long distances.

**Technical Parameters**:
- **Resolution**: Matches PAL with resolutions like **720 × 576**.
- **Frame Rate**: Operates at **25 Hz**, similar to PAL.
- **Lines**: Uses **625 lines per frame** for high resolution.

**Color Encoding**:  
SECAM transmits chrominance information sequentially:

- U and V components are sent on alternate lines.
- A memory system stores color data for interpolation.  
    This method eliminates phase errors, making it more reliable in poor transmission conditions.

**The countries that support SECAM are as follows:** 
Afghanistan, Benin, Burkina Faso, Bulgaria, Burundi, Central African Republic, Chad, Congo, Czechoslovakia, Djibouti, Egypt, France, French Guiana, Gabon, Greece, Guadalupe, Guinea, Gyprus, Haiti, Hungary, Iran, Iraq, Ivory Coast, Lebanon, Libya, Madagascar, Mali, Martinique, Mauritius, Mauritania, Monaco, Morocco, Niger, North Korea, Poland, Russia, Rwanda, Saudi Arabia, Senegal, Syria , Togo, Tunisia, Vietnam, Western Samoa, Zaire

**Advantages**:
1. Excellent resilience to signal degradation.
2. Reliable in long-distance and weak-signal conditions.

**Disadvantages**:
1. Sequential color transmission can lead to slower processing.
2. Limited compatibility with NTSC and PAL systems.

##### Comparison of NTSC, PAL, and SECAM

|**Attribute**|**NTSC**|**PAL**|**SECAM**|
|---|---|---|---|
|**Lines Per Frame**|525|625|625|
|**Frame Rate**|29.97 Hz|25 Hz|25 Hz|
|**Color Encoding**|YIQ|YUV|Sequential (U, V)|
|**Resolution**|Lower|Higher|Higher|
|**Resilience**|Low (phase errors)|Moderate|High|
|**Regions Used**|North America, Japan|Europe, Asia, Australia|France, Russia, Africa|

##### Compatibility with Color Television:
Compatibility implies that the colour television signal must produce a normal black and white picture on a monochrome receiver without any modification of the receiver circuitry and a color receiver must be able to produce a black and white picture from a normal monochrome signal. This is referred to as reverse compatibility.
##### Requirements for Compatibility:
1. It should occupy the same bandwidth as the corresponding monochrorne signal.
2. The location and spacing of picture and sound carrier frequencies should remain the same.
3. The color signal should have the same luminance (brightness) information as would a monochrome signal, transmitting the same scene.
4. The composite colour signal should contain color information together with the ancillary signals needed to allow this to be decoded.
5. The colour information should be carried in such a way that it does not affect the picture reproduced on the screen of a monochrome receiver.
6. The system must employ the same deflection frequencies and sync signals as used for monochrome transmission and reception.


#### Module 3.2: Advanced TV Systems
##### High Definition TV (HDTV)
HDTV is a digital broadcasting standard that offers improved picture quality over standard definition television (SDTV). It uses advanced encoding techniques for higher resolutions and better color depth.

**Key Features**:
1. **Resolutions**:
    - **720p**: Progressive scan, 1280 × 720 pixels.
    - **1080i**: Interlaced scan, 1920 × 1080 pixels.
    - **1080p**: Progressive scan, 1920 × 1080 pixels.
2. **Aspect Ratio**: Widescreen **16:9**, compared to the 4:3 aspect ratio of SDTV.
3. **Audio**: Enhanced audio quality using surround sound formats like Dolby Digital.

**Applications**:  
Used in digital broadcasting, Blu-ray media, and streaming platforms like Netflix.

##### 3D Television
3D TV adds depth to the viewing experience by providing separate images for each eye, creating a stereoscopic effect.

**Key Features**:
1. **Active 3D**: Uses shutter glasses synchronized with the TV to provide alternate images to each eye.
2. **Passive 3D**: Uses polarized glasses to separate images for each eye.
3. **Glasses-Free 3D**: Employs lenticular lenses for autostereoscopic viewing.

**Applications**:  
Primarily used for 3D movies, gaming, and immersive content.