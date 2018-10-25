Poisson Blending
================

## Toy Problem

To perform Poisson Blending, we proceeded with the Toy Problem to restore the original image from zero image with minimal gradient from the original image.
To obtain an image satisfying all three equations, we wrote the source code as shown below.
Denote the intensity of the source image at (x,y) as s(x,y), and the values of the image to solve for as v(x,y). 

![image](https://user-images.githubusercontent.com/44015662/47510708-a2fc7600-d8b3-11e8-8f29-a19b82ea8faa.png)


``` 
I = double(imread('toy_problem.png'));
[imh, imw, nn] = size(I);
 
Im2var = zeros(imh,imw);
Im2var(1:imh*imw) = 1:imh*imw;
 
A = sparse([],[],[],1+(imw-1)*imh+(imh-1)*imw,imw*imh);
 
b(1) = I(1,1);
A(1,:) = zeros(1,imh*imw);
A(1,1) = 1;
 
for k=1:(imw-1)*imh+(imh-1)*imw
    k
    if k < (imw-1)*imh + 1
        
        y = floor(1+(k-1)/imw);
        x = 1+mod(k-1,imw-1);
        
        A(k+1,Im2var(y,x+1)) = 1;
        A(k+1,Im2var(y,x)) = -1;
        b(k+1) = I(y,x+1) - I(y,x);
    else
        k_temp = k-imh*(imw-1);
        y = 1+mod(k_temp-1,imh-1);
        x = floor(1+(k_temp-1)/imh);
        
        A(k+1,Im2var(y+1,x)) = 1;
        A(k+1,Im2var(y,x)) = -1;
        b(k+1) = I(y+1,x) - I(y,x);
    end
end
 
v = A\b';
v = reshape(v,[119,110]);
imshow(v,[])
```

Since Matrix A is sparse, we use MATLAB’s sparse function to initialize it so that the \ operator can run fast. The results of the Toy Problem is as follows. From the left are the original image, the output image and the error image of the two images.

## Poisson Blending with Mixed Gradients

## Your Own Examples
