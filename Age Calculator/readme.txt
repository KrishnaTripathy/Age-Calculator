1. new Date().toISOString(): new Date() creates a new JavaScript Date object representing the current date and time. 
.toISOString() converts the Date object to a string in ISO format, which looks like this: "YYYY-MM-DDTHH:mm:ss.sssZ". This format includes the date, time, and timezone information.

2. .split("T"): .split("T") is a method that splits the string into an array of substrings using the "T" character as the separator. After the split, you get an array with two elements: the date part before "T" and the time part after "T".


3. [0]: [0] retrieves the first element of the array, which is the date part.

4. "userInput.max = ...": userInput refers to an HTML input element, likely of type "date". 
The .max attribute sets the maximum allowed value for the date input.

Putting it all together, the line of code sets the maximum date for the input element to the current date. It extracts the date part from the ISO string format and assigns it to the max attribute. This ensures that users cannot select a date beyond the current date when using the input field.



// Get the input element with id "date" from the HTML document
let userInput = document.getElementById("date");

// Set the maximum allowed date for the input field to today's date
userInput.max = new Date().toISOString().split("T")[0];

// Get the element with id "result" from the HTML document
let result = document.getElementById("result");

// Define a function named calculateAge
function calculateAge() {
    // Retrieve the birth date entered by the user and convert it to a Date object
    let birthDate = new Date(userInput.value);

    // Extract day, month, and year components from the birth date
    let d1 = birthDate.getDate();            // Day of the month (1-31)
    let m1 = birthDate.getMonth() + 1;       // Month (0-11, hence adding 1 to get 1-12)
    let y1 = birthDate.getFullYear();        // Year (four digits)

    // Get today's date
    let today = new Date();

    // Extract day, month, and year components from today's date
    let d2 = today.getDate();                // Day of the month (1-31)
    let m2 = today.getMonth() + 1;          // Month (0-11, hence adding 1 to get 1-12)
    let y2 = today.getFullYear();           // Year (four digits)

    let d3, m3, y3;

    // Calculate the age in years, months, and days
    y3 = y2 - y1;                            // Calculate the difference in years
    if (m2 >= m1) {
        m3 = m2 - m1;                        // Calculate the difference in months
    } else {
        y3--;                               // Adjust the years if the current month is less than birth month
        m3 = 12 + m2 - m1;                   // Calculate the difference in months considering the previous year
    }
    if (d2 >= d1) {
        d3 = d2 - d1;                        // Calculate the difference in days
    } else {
        m3--;                                // Adjust the months if the current day is less than birth day
        d3 = getDaysInMonth(y1, m1) + d2 - d1;  // Calculate the difference in days considering the previous month
    }
    if (m3 < 0) {
        m3 = 11;                             // Adjust the months to 11 if they are less than 0
        y3--;                               // Adjust the years if the current month is less than birth month
    }

    // Update the HTML content with the calculated age
    result.innerHTML = `You are <span>${y3}</span> years, <span>${m3}</span> months and <span>${d3}</span> days old`;
}

// Function to get the number of days in a given month of a specific year
function getDaysInMonth(year, month) {
    return new Date(year, month, 0).getDate();
}
