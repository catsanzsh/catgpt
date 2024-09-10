// ==UserScript==
// @name        Project Orion
// @version     1.1
// @license     MIT
// @description Automates file uploading process for various models on specified websites.
// @author      Pro-Fessional
// @match       *://example.com/*  // Change this to the website's URL where you want to upload files
// @grant       none
// @run-at      document-end
// @namespace   https://greasyfork.org/users/1090501
// ==/UserScript==

(function () {
    'use strict';

    // Function to trigger file upload
    function triggerFileUpload(filePath, selector) {
        const input = document.querySelector(selector || 'input[type="file"]');  // Use custom selector if provided
        if (input) {
            // Create a new DataTransfer object to handle the file
            const dataTransfer = new DataTransfer();
            const file = new File([new Blob(['file content'])], filePath, { type: 'application/octet-stream' });
            dataTransfer.items.add(file);
            input.files = dataTransfer.files;
            input.dispatchEvent(new Event('change', { bubbles: true }));
        } else {
            console.error('File input element not found.');
        }
    }

    // Function to handle different models
    function handleModelUpload(model = 'Omni Mini') {  // Default to 'Omni Mini'
        const currentVersion = '4.10.24'; // Current version of the model
        const baseFilePath = `model-file-${currentVersion}.txt`; // Dynamic file name based on version

        switch (model) {
            case 'GPT-3':
                triggerFileUpload(`gpt3-${baseFilePath}`, '#gpt3-file-input');  // Replace with actual selector
                break;
            case 'GPT-4':
                triggerFileUpload(`gpt4-${baseFilePath}`, '#gpt4-file-input');  // Replace with actual selector
                break;
            case 'Omni Mini':
                triggerFileUpload(`omni-mini-${baseFilePath}`, '#omni-mini-file-input');  // Replace with actual selector
                break;
            default:
                console.error('Model not recognized.');
                break;
        }
    }

    // Example usage: handle upload for default model 'Omni Mini'
    handleModelUpload();  // Defaults to 'Omni Mini'

})();
