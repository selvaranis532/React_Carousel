# Ex05 Image Carousel
## Date:

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
## App.jsx
```
import Carousel from "./Carousel";

function App() {
  return (
    <div>
      <Carousel />
    </div>
  );
}

export default App;
```
## Carousel.jsx
```
import { useState, useEffect } from "react";
import "./Carousel.css";

function Carousel() {

  const images = [
    "https://picsum.photos/id/1015/800/400",
    "https://picsum.photos/id/1016/800/400",
    "https://picsum.photos/id/1018/800/400",
    "https://picsum.photos/id/1020/800/400",
    "https://picsum.photos/id/1024/800/400"
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  // Next Slide
  const nextSlide = () => {
    setCurrentIndex((prevIndex) =>
      (prevIndex + 1) % images.length
    );
  };

  // Previous Slide
  const prevSlide = () => {
    setCurrentIndex((prevIndex) =>
      (prevIndex - 1 + images.length) % images.length
    );
  };

  // Auto Slide
  useEffect(() => {

    const interval = setInterval(() => {
      nextSlide();
    }, 3000);

    return () => clearInterval(interval);

  }, []);

  return (
    <div className="carousel-container">

      <h2>Advanced React Image Carousel</h2>

      <div className="carousel">

       

        {/* Image */}
        <img
          src={images[currentIndex]}
          alt="slide"
          className="carousel-image"
        />


      </div>

      {/* Dots */}
      <div className="dots">

        {images.map((_, index) => (

          <span
            key={index}
            className={
              currentIndex === index
                ? "dot active"
                : "dot"
            }

            onClick={() => setCurrentIndex(index)}
          ></span>

        ))}

      </div>

    </div>
  );
}

export default Carousel;
```
## Carousel.css
```
body {
  margin: 0;
  padding: 0;
  background: #f2f2f2;
  font-family: Arial, sans-serif;
}

.carousel-container {
  width: 70%;
  margin: 40px auto;
  text-align: center;
}

.carousel {
  position: relative;
}

.carousel-image {
  width: 100%;
  height: 400px;
  border-radius: 10px;
}

.prev,
.next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0,0,0,0.5);
  color: white;
  border: none;
  padding: 12px;
  font-size: 24px;
  cursor: pointer;
  border-radius: 50%;
}

.prev {
  left: 10px;
}

.next {
  right: 10px;
}

.dots {
  margin-top: 15px;
}

.dot {
  height: 12px;
  width: 12px;
  margin: 5px;
  background: gray;
  border-radius: 50%;
  display: inline-block;
}

.active {
  background: black;
}
```

## OUTPUT
<img width="1919" height="981" alt="Screenshot 2026-05-22 185629" src="https://github.com/user-attachments/assets/83257fb1-a463-43f9-a35a-670ca9345b1b" />
<img width="1919" height="938" alt="Screenshot 2026-05-22 190123" src="https://github.com/user-attachments/assets/84a63966-5e22-4c68-9dd7-dadfb3d99ffc" />
<img width="1908" height="926" alt="Screenshot 2026-05-22 190208" src="https://github.com/user-attachments/assets/9fb194c6-cc22-4743-8e23-39b6e91c51e8" />



## RESULT
The program for creating Image Carousel using React is executed successfully.
