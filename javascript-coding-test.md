<div class="container">
    <h1>Q1. Write a program in javascript. sum(2)(3); // Expected output is 5</h1>
    <div class="highlightCode">
        <pre>
            function sum(x, y) {
                if (y !== undefined) {
                  return x + y;
                } else {
                  return function (y) {
                    return x + y;
                  };
                }
              }
        </pre>
    </div>
    <p>Output</p>
    <pre>
        console.log(sum(2,3));   // Outputs 5
        console.log(sum(2)(3));  // Outputs 5
    </pre>
</div>