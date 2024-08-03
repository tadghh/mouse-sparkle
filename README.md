# mouse-sparkle

```js
// ==UserScript==
// @name         Mouse Trail Stars
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  Makes stars follow behind the mouse cursor
// @author       Your Name
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // CSS for the star elements
    const styles = `
        .star {
            position: absolute;
            width: 10px;
            height: 10px;
            background: yellow;
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            pointer-events: none;
            opacity: 0.8;
            animation: fadeOut 1s forwards;
            z-index: 2147483647; /* Ensures the stars appear above other content */
        }

        @keyframes fadeOut {
            to {
                opacity: 0;
                transform: translateY(-20px);
            }
        }
    `;

    // Append the styles to the head of the document
    const styleSheet = document.createElement('style');
    styleSheet.type = 'text/css';
    styleSheet.innerText = styles;
    document.head.appendChild(styleSheet);

    // Function to create a star element at the cursor position
    function createStar(x, y) {
        const star = document.createElement('div');
        star.className = 'star';
        star.style.left = `${x}px`;
        star.style.top = `${y}px`;

        document.body.appendChild(star);

        // Remove the star after the animation ends
        setTimeout(() => {
            star.remove();
        }, 1000);
    }

    // Event listener for mouse movement
    document.addEventListener('mousemove', (event) => {
        createStar(event.pageX, event.pageY);
    });
})();

```
