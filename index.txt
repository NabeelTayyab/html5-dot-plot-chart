// Data Related Global Variables
const divisons = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12], // Divisons to be drawn
    answerDots = [6, 2, 3, 5, 2, 5, 0, 0, 2, 10, 7, 4, 1], // Answer dots 
    axisName = 'Minutes To Eat Breakfast', // Axis Name for Chart - x-axis
    mode = 1; // Set Mode Value here to change mode, mode can be 1 or 2

// Chart Related Global Variables
const gridSize = 40, // Set Grid Size to 40px, Grid is an single unit of chart/dot plot
    x_axis_distance_grid_lines = 13, // Total lines after which  x axis is declared
    y_axis_distance_grid_lines = 1, // Total lines after which y axis is declared
    x_axis_starting_point = {
        number: 1
    },
    circle_color_mode_1 = "green",
    circle_color_mode_2 = "gray";

var canvas = document.getElementById("dotPlots"), // Get Canvas Element
    ctx = canvas.getContext("2d"), // Get the Canvas Context
    canvas_width = canvas.width, // Get Canvas width
    canvas_height = canvas.height; // Get Canvas height

if (mode === 1) {
    draw_horizontal_line(); // Draw Grid/Horizontal Lines/ X-Axis
    draw_ticks(); // Draw Ticks/ Markers
    print_circles_module_one(); // Draw Answer Dots/ Circles for Mode 1
    ctx.fillText(axisName, 243, 38); // Print the Name of Axis
} else if (mode === 2) {
    draw_horizontal_line(); // Draw Grid/Horizontal Lines/ X-Axis
    draw_ticks(); // Draw Ticks/ Markers
    print_circles_module_two(); // Draw Answer Dots/ Circles for Mode 2
    ctx.fillText(axisName, 243, 38); // Print the Name of Axis
}

///////////////////////////////////////////////////////////////////////////
//              Functions used in this page
///////////////////////////////////////////////////////////////////////////

///////////////////////////////////////////////////////////////////////////
// Function to draw ticks/markers on horizontal  axis line
function draw_ticks() {
    // Ticks marks along the positive X-axis
    for (i = 0; i < divisons.length; i++) {
        ctx.beginPath(); // Begin Path
        ctx.lineWidth = 3; // Set Line Width 
        ctx.strokeStyle = "#000000"; // Set Color of Line

        // Draw a tick mark 12px long (-6 to 6)
        ctx.moveTo(gridSize * i, -6); // Start
        ctx.lineTo(gridSize * i, 6); // End
        ctx.stroke();

        // Text value at that point
        ctx.font = '14px Arial Bold'; // Set Font Size and Font Family
        ctx.textAlign = 'center'; // Set Text Alignment
        ctx.fillText(divisons[i], gridSize * i, 19); // Print the text on screen
    }
};

/////////////////////////////////////////////////////////////////////////////
//          Function to draw Horizontal lines/ x-Axis Line
function draw_horizontal_line() {
    // Draw grid lines along X-axis
    for (var i = 0; i <= answerDots.length; i++) {
        ctx.beginPath(); // Begin Path 
        ctx.lineWidth = 3; // Set Line Width

        // If line represents X-axis draw in different color
        if (i == x_axis_distance_grid_lines)
            ctx.strokeStyle = "#000000"; // If the current line is x-axis 
        else
            ctx.strokeStyle = "#FFFFFF"; // If current line is any of the lines above x-axis 

        // If Current line is x-axis line
        if (i == answerDots.length) {
            ctx.moveTo(gridSize, gridSize * i);
            ctx.lineTo(gridSize * divisons.length, gridSize * i);
        } else {
            // If current line is any of the lines above x-axis
            ctx.moveTo(gridSize, gridSize * i + 0.5);
            ctx.lineTo(gridSize * divisons.length, gridSize * i + 0.5);
        }
        ctx.stroke();
    }
    // Translate origin to x-axis (new one, bottom)
    ctx.translate(y_axis_distance_grid_lines * gridSize,
        x_axis_distance_grid_lines * gridSize);
}

/////////////////////////////////////////////////////////////////////////////////
//          Function to print circles/ Answer Dots
function print_circles_module_one() {
    // Go through each marker / divison at a time
    for (let index = 0; index < divisons.length; index++) {
        // Go through each answer dots array value at a time
        // Run for about each elements value ex 1st element is 6 so it should loop 6 times
        for (i = 0; i < answerDots[index]; i++) {
            // Invoke draw_circle function by passing x, y, radius and fill paramters
            draw_circle(gridSize * index, -(i * 30) - 20, 10, circle_color_mode_1);
        }
    };
}

//////////////////////////////////////////////////////////////////////////////////
//          Function to print circles/ Answer Dots
function print_circles_module_two() {
    // Go through each marker / divison at a time
    for (let index = 0; index < divisons.length; index++) {
        // Go through each answer dots array value at a time
        // Run for about each elements value ex 1st element is 6 so it should loop 6 times
        for (i = 0; i < divisons.length; i++) {
            // Invoke draw_circle function by passing x, y, radius and fill paramters
            draw_circle(gridSize * index, -(i * 30) - 20, 10, circle_color_mode_2);
        }
    };
}

///////////////////////////////////////////////////////////////////////////////////
//          Function to draw circle on canvas
//          Takes in x & y coordinates, desired radius and desired color for circle
function draw_circle(xAxis, yAxis, radius, fill) {
    ctx.beginPath(); // Begin path
    ctx.fillStyle = fill; // Set Fill 
    ctx.arc(xAxis, yAxis, radius, 0, Math.PI * 2); // create a with 0 degree start point and end on the same point so as to create a circle
    ctx.fill(); // Fill color in circle
}

//////////////////////////////////////////////////////////////////////////////////////////////////////
//                                              EOF
//////////////////////////////////////////////////////////////////////////////////////////////////////