### There are three important two-dimensional arrays:
 - vertices
   - this array holds each point of the loaded shape.
   - we are not supposed to modify this array.
 - ctrans
   - this array holds the composed transformation matrix
   - each time it draws it will apply this transformation to the vertices to get the scrnpts (the third array)
 - scrnpts
   - this array holds the points to draw.
### There are helper classes to form and hold a transformation matrix
 - the mMatrix
   - this is an instance of MMatrix class
   - this holds the transformation matrix as the ctrans array does but in an more Oboject-Oriented way.

### How we manage to apply a transformation to draw?
 - follow these steps:
   - create an MMatrix instance
     - e.g. var MMatrix n = new MMatrix(4, 4);
   - initialize it to an identity matrix
     - e.g. n.setIdentity();
     - this will set this matrix to
       | 1 0 0 0|
       | 0 1 0 0|
       | 0 0 1 0|
       | 0 0 0 1|
   - setup the MMatrix for a transformation
     - e.g. setup and translation matrix 100 in x, -20 in y, and 30 in z.
       - n.Set(3, 0, 100) // Set(row, column, value)
       - n.Set(3, 1, -20)
       - n.Set(3, 2, 30)
   - we need to add it to the current transformation
    - so we multiply this.mMatrix by n
      - this.mMatrix = this.mMatrix.multiply(n)
    - now this.mMatrix is udpated but we need to update this.ctrans in order to apply it on next draw
      - this.updateTrans(this.mMatrix)
   - then the program will draw a new shape with the new transformation
 
 ### What we need to add new tranformation?
   - create a new function to apply the transformation
   - inside the function body, do the steps above
   - find the line that handle to button clicked event and call your new transformation function there
     - e.g. `if (e.Button == transupbtn)` this is to handle the translate up button event.
     - add code to call your function to add the tranformation after that line
 
 ### Other functions to pay attention to
   - invalidate()
     - this built-in function is used to redraw
     - I think when we do a 'animation' - continuous tranformation, we need to call the invalidate()
   - GetShapeRect()
     - I create this function to get the area (rectangle) of the current shape
       - it returns a Rect object which has properties defined as:
         - x: horizontal position, goes from left to right
         - y: vertical position, goese from top to bottom
         - width: the width of the currently drawing shape
         - height: the height of the currently drawing shape
   - RestoreInitialImage()
     - the project function where is bascially your entry point. A good place to add a breakpoint to peek into when you debug this program.
