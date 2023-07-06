# React-Framify

React-Framify is a lightweight and versatile React component library that provides device framesets for showcasing screenshots and images. This library offers an updated and optimized version of the popular reac-device-frameset, with enhanced features and compatibility.

## Features
- Supports the iPhone 14 Pro frameset.
- Enables easy navigation between multiple screenshots or images.
- Provides touch swipe gestures for seamless image browsing.
- Optimized for performance and smooth animations.
- Compatible with both ReactJS and ReactTS.

## Installation
To use React Device Frameset in your React project, follow these steps:

1. Manually copy the required files into your project directory.
   - For JavaScript (JS) projects:
     ```jsx
     import React, { useEffect, useState } from 'react';
      import PhoneFrameset from '../assets/iphone-14-pro.png';

      const PhoneFrame = ({ screenshotList }) => {
        const [currentImageIndex, setCurrentImageIndex] = useState(0);
        const [initialTouchPosition, setInitialTouchPosition] = useState(null);
        const [fadeOut, setFadeOut] = useState(false);

        useEffect(() => {
          setCurrentImageIndex(0); // Reset the current image index when screenshotList changes
        }, [screenshotList]);

        const handleTouchStart = (e) => {
          const touch = e.touches[0];
          setInitialTouchPosition(touch.clientX);
        };

        const handleTouchMove = (e) => {
          if (!initialTouchPosition) return;

          const touch = e.touches[0];
          const currentTouchPosition = touch.clientX;
          const touchDistance = currentTouchPosition - initialTouchPosition;

          if (touchDistance > 50) {
            // Swipe right, show previous image
            showPreviousImage();
          } else if (touchDistance < -50) {
            // Swipe left, show next image
            showNextImage();
          }
        };

        const handleTouchEnd = () => {
          setInitialTouchPosition(null);
        };

        const showPreviousImage = () => {
          setFadeOut(true);
          setTimeout(() => {
            setCurrentImageIndex((prevIndex) =>
              prevIndex === 0 ? screenshotList.length - 1 : prevIndex - 1
            );
            setFadeOut(false);
          }, 300);
        };

        const showNextImage = () => {
          setFadeOut(true);
          setTimeout(() => {
            setCurrentImageIndex((prevIndex) =>
              prevIndex === screenshotList.length - 1 ? 0 : prevIndex + 1
            );
            setFadeOut(false);
          }, 300);
        };

        return (
          <figure
            className="phone__frameset--wrapper preview__phone--mockup"
            onTouchStart={handleTouchStart}
            onTouchMove={handleTouchMove}
            onTouchEnd={handleTouchEnd}
          >
            <img src={PhoneFrameset} alt="Image by svstudioart on Freepik" className="phone__frameset" />
            <img
              src={screenshotList[currentImageIndex]}
              alt=""
              className={`phone__frameset--img ${fadeOut ? 'fade-out' : ''}`}
            />
            <div className="preview__scroll--btns">
              <button className="preview__scroll--btn btn" onClick={showPreviousImage}>Previous</button>
              <button className="preview__scroll--btn btn" onClick={showNextImage}>Next</button>
            </div>
          </figure>
        );
      };

      export default PhoneFrame;
     ```
     - Copy the `PhoneFrame.css` file into your project's CSS directory from the `./src/PhoneFrame.css`.
   - For TypeScript (TS) projects:
     ```tsx
      import React, { useEffect, useState } from 'react';
      import '../dist/PhoneFrame.css';

      // Declare the image variable
      const PhoneFrameset: any = require('../assets/iphone-14-pro.png');


      export interface PhoneFrameProps {
        screenshotList: string[]; // Array of strings representing image file names
      }

      const PhoneFrame: React.FC<PhoneFrameProps> = ({ screenshotList }) => {
        const [currentImageIndex, setCurrentImageIndex] = useState(0);
        const [initialTouchPosition, setInitialTouchPosition] = useState<number | null>(null); // Add type annotation
        const [fadeOut, setFadeOut] = useState(false);

        useEffect(() => {
          setCurrentImageIndex(0); // Reset the current image index when screenshotList changes
        }, [screenshotList]);

        useEffect(() => {
          setCurrentImageIndex(0); // Reset the current image index when screenshotList changes
        }, [screenshotList]);

        const handleTouchStart = (e: React.TouchEvent) => {
          const touch = e.touches[0];
          setInitialTouchPosition(touch.clientX);
        };

        const handleTouchMove = (e: React.TouchEvent) => {
          if (!initialTouchPosition) return;

          const touch = e.touches[0];
          const currentTouchPosition = touch.clientX;
          const touchDistance = currentTouchPosition - initialTouchPosition;

          if (touchDistance > 50) {
            // Swipe right, show previous image
            showPreviousImage();
          } else if (touchDistance < -50) {
            // Swipe left, show next image
            showNextImage();
          }
        };

        const handleTouchEnd = () => {
          setInitialTouchPosition(null);
        };

        const showPreviousImage = () => {
          setFadeOut(true);
          setTimeout(() => {
            setCurrentImageIndex((prevIndex) =>
              prevIndex === 0 ? screenshotList.length - 1 : prevIndex - 1
            );
            setFadeOut(false);
          }, 300);
        };

        const showNextImage = () => {
          setFadeOut(true);
          setTimeout(() => {
            setCurrentImageIndex((prevIndex) =>
              prevIndex === screenshotList.length - 1 ? 0 : prevIndex + 1
            );
            setFadeOut(false);
          }, 300);
        };

        return (
          <figure
            className="phone__frameset--wrapper preview__phone--mockup"
            onTouchStart={handleTouchStart}
            onTouchMove={handleTouchMove}
            onTouchEnd={handleTouchEnd}
          >
            <img src={PhoneFrameset} alt="Image by svstudioart on Freepik" className="phone__frameset" />
            <img
              src={screenshotList[currentImageIndex]}
              alt=""
              className={`phone__frameset--img ${fadeOut ? 'fade-out' : ''}`}
            />
            <div className="preview__scroll--btns">
              <button className="preview__scroll--btn btn" onClick={showPreviousImage}>Previous</button>
              <button className="preview__scroll--btn btn" onClick={showNextImage}>Next</button>
            </div>
          </figure>
        );
      };

      export default PhoneFrame;
     ```
     - Copy the `PhoneFrame.css` file into your project's CSS directory from the `./src/PhoneFrame.css`.

2. Import the `PhoneFrame` component in your app.
   - For JavaScript (JS) projects:
     ```jsx
     import React from 'react';
     import PhoneFrame from './components/PhoneFrame';
     import screenshot1 from './assets/screenshot1.png';
     import screenshot2 from './assets/screenshot2.png';

     const App = () => {
       const screenshotList = [screenshot1, screenshot2];

       return (
         <div>
           <PhoneFrame screenshotList={screenshotList} />
           {/* Rest of your app code */}
         </div>
       );
     };

     export default App;
     ```

   - For TypeScript (TS) projects:
     ```tsx
     import React from 'react';
     import PhoneFrame, { PhoneFrameProps } from './components/PhoneFrame';
     import screenshot1 from './assets/screenshot1.png';
     import screenshot2 from './assets/screenshot2.png';

     const App: React.FC = () => {
       const screenshotList: string[] = [screenshot1, screenshot2];

       return (
         <div>
           <PhoneFrame screenshotList={screenshotList} />
           {/* Rest of your app code */}
         </div>
       );
     };

     export default App;
     ```

3. Ensure that the necessary CSS file is imported in your project.
   - For JavaScript (JS) projects:
     ```jsx
     import './css/PhoneFrame.css';
     ```

   - For TypeScript (TS) projects:
     ```tsx
     import '../dist/PhoneFrame.css';
     ```

4. Run your React application and enjoy using the React Device Frameset!

## Usage
The `PhoneFrame` component is the main component of the React Device Frameset library. It accepts the following props:
- `screenshotList` (array of strings): An array of image file paths or URLs representing the screenshots or images to be displayed within the frameset.

Here's an example of using the `PhoneFrame` component with screenshots:
```jsx
<PhoneFrame screenshotList={screenshotList} />
