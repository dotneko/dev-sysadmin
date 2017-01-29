*Notes on Octave taken from [Andrew Ng's Coursera machine Learning Course](https://www.coursera.org/learn/machine-learning)*

# Basic commands

```
ones()
zeros()
eye()
size(A)
length(A)   % Usually applied to vectors
```

# Chaining commands
- Use `,` to chain commands with output.
- Use `;` to chain commands without output.

# Navigation

```
pwd
cd
ls
```

# Loading & saving data

```
load filename1.dat
load('filename1.dat')       % equivalent to above

save filename2.mat
save filename3.mat v        % stores data in binary
save hello.txt v -ascii     % save as text(ASCII)
```

# Viewing variables in current scope

```
who
whos                        % shows detailed view
```

# Removing data

```
clear                       % clears all data
clear variable_name
```

# Manipulating data

```
A=[1 2; 3 4; 5 6]
A(3,2)                      % Retrieves item in row 3, column 2
A(2,:)                      % Colon (:) means every element along that row/column A(2,:) retrieves all elements in row 2
A(:,2)                      % Retrieves all elements in column 2
```

# Assigning elements

```
A(:,2) = [10;11;12]         % Assigns 10,11,12 to the second column
```

# Appending vectors

```
A = [A,[100, 101, 102]]
A(:)                        % Put all elements of A into a single vector
```

# Concatenating matrices

```
A=[1 2;3 4;5 6]
B=[11 12;13 14;15 16]
C=[A B]                     % Concatenates matrices side by side
C=[A;B]                     % Concatenates matrices vertically
```

# Computing on data

```
A=[1 2;3 4;5 6]
B=[11 12;13 14;15 16]
C=[1 1;2 2]

A*C (3x3 * 2x3 matrix, gives a 3x2 matrix)
```

# Elementwise operations

```
A .* B                      % Takes each element in A and multiples by corresponding element in B
A .^ 2                      % Element squaring of A

v = [1; 2; 3]
1 ./ v                      % Elementwise reciprical of v
1 ./ A                      % Elementwise reciprical of matrix A

log(v)                      % Elementwise logarithm
exp(v)
abs(v)
-v                          % Same as -1 * v

v + ones(length(v),1)       % Increments all elements of v by 1
```

# Tranposing etc.

```
A = [1 2; 3 4; 5 6]
A'                          % Represents A transpose, i.e. [1 3 5;2 4 6]
(A')'                       % Returns transpose of A transpose, i.e. A

a = [1 15 2 0.5]
val = max(a)                % Returns maximum value of a, i.e. 15
[val,ind] = max(a)          % Returns maximum value of a and its index
max(A)                      % Does columnwise maximum

a < 3                       % Does elementwise comparison

magic(3)                    % Generates a 3x3 matrix with magic squares

[r,c] = find(A >= 7)        % r is row, c is column
sum(a)
prod(a)
floor(a)                    % rounds up
ceil(a)                     % rounds down
max(rand(3), rand(3))

pinv(A)                     % pseudo inverse of A
```

# Plotting Data

```
t=[0:0.01:0.98];
y1=sin(2*pi*4*t);
plot(t,y1);
plot(t,y2);
```

## Plot two sets of data into one plot

```
plot(t,y1);
hold on;                    % Holds previous plot
plot(t,y2,'r');              % r indicates red color
xlabel('time')
ylabel('value')
legend('sin', 'cos')
title('my plot')
```

## Save file as PNG

```
print -dpng 'myPlot.png'
```

## Using figures for multiple plots

```
figure(1); plot(t,y1);
figure(2); plot(t,y2);
subplot(1,2,1);             % Divides plot to a 1x2 grid, access first element.
plot(t,y1);
subplot(1,2,2);
plot(t,y2);
axis([0.5 1 -1 1])
```

## Clear a figure
```
clf
```

## Using a grid of colors
```
A = magic(5)

imagesc(A)
```

## Display grid of gray colors
```
imagesc(A), colorbar, colormap gray;
imagesc(magic(15)), colorbar, colormap gray;
```

# Writing Control Statemnents

## For Loop Example
```
v=zeros(10,1)

% Spacing doesn't matter
for i=1:10,
  v(i) = 2^i;
end;

indicies=1:10;
for i=indicies,
  disp(i);
end;
```

## While Loop Example
```
i=1;
while i <= 5;
  v(i) = 100;
  i = i + 1;
end;
```

## Break Example
- Overwriting the first 5 values with 999.
```
i=1;
while true,
  v(i) = 999;
  i = i+1;
  if i == 6,
    break;
  end;
end;
```

## Example of `Elseif` and `Else`
```
v(1) = 2;
if v(1) ==1,
  disp('The value is one');
elseif v(1) == 2,
  disp('The value is two');
else
  disp('The value is not one or two');
```

# Defining Functions

- Create a file with filename as function name and extension `.m`
- To run the function, need to `cd` into directory that contains the function before running the function.

```
% Filename: squareThisNumber.m

function y = squareThisNumber(x)
y=x^2;
```

## Example function

```
% Filename: squareAndCubeThisNumber.m

function [y1,y2] = squareAndCubeThisNumber(x)

y1 = x^2
y2 = x^3
```

## Defining the Octave search path

```
addpath('C:\Users\username\Desktop')
```

## Example to define a cost function

```
% Filename: costFunctionJ.m

function J = costFunctionJ(X, y, theta)

% X is the "design matrix" containing the training example
% y is the class labels

m = size(X, 1);             % number of training examples
predictions = X * theta     % predictions of hypothesis on all m examples
sqrErrors = (predictions - y).^2;   % squared errors

J = 1 / (2*m) * sum(sqrErrors);
```

## Testing the cost function

```
X = [1 1;1 2;1 3]
y = [1; 2; 3]
```

# Vectorization
- Note that Matlab/Octave vectors are indexed from 1.

```
prediction = theta' * x;
```
