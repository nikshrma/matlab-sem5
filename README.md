# UMC513 — MATLAB solutions for Labsheets 1–4

Each code block includes its own inputs. Run any block independently. For the two questions that explicitly ask for a function, paste the entire block into a new MATLAB script and run it. Blocks marked **Symbolic Math Toolbox** require that toolbox.

## Labsheet 1

### Matrix operations

#### Question 1 — Create A and B

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];
B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];
```

#### Question 2 — Check matrix sizes

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

disp(size(A))   % [3 3]
disp(size(B))   % [3 5]
```

#### Question 3 — Display the first two rows of A

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

disp(A(1:2, :))
```

#### Question 4 — Display the last three columns of B

**Built-in solution**

```matlab
B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

disp(B(:, end-2:end))
```

#### Question 5 — Determinant and inverse of A

**Manual solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

M = A;

cofactors = zeros(3);
for i = 1:3
    rows = [1:i-1 i+1:3];
    for j = 1:3
        cols = [1:j-1 j+1:3];
        S = M(rows, cols);
        cofactors(i,j) = (-1)^(i+j) * ...
            (S(1,1)*S(2,2) - S(1,2)*S(2,1));
    end
end

d = 0;
for j = 1:3
    d = d + M(1,j)*cofactors(1,j);
end

Ainv = [];
if d ~= 0
    Ainv = cofactors.' / d;
end

disp(d)
disp(Ainv)
```

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

disp(det(A))
disp(inv(A))
```

#### Question 6 — Determinant and inverse of the transpose of A

**Manual solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

M = zeros(size(A,2),size(A,1));
for i = 1:size(A,1)
    for j = 1:size(A,2)
        M(j,i) = A(i,j);
    end
end

cofactors = zeros(3);
for i = 1:3
    rows = [1:i-1 i+1:3];
    for j = 1:3
        cols = [1:j-1 j+1:3];
        S = M(rows, cols);
        cofactors(i,j) = (-1)^(i+j) * ...
            (S(1,1)*S(2,2) - S(1,2)*S(2,1));
    end
end

d = 0;
for j = 1:3
    d = d + M(1,j)*cofactors(1,j);
end

Ainv = [];
if d ~= 0
    Ainv = cofactors.' / d;
end

disp(d)
disp(Ainv)
```

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

At = A.';
disp(det(At))
disp(inv(At))
```

#### Question 7 — Powers and products

**Manual solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

M = A;

cofactors = zeros(3);
for i = 1:3
    rows = [1:i-1 i+1:3];
    for j = 1:3
        cols = [1:j-1 j+1:3];
        S = M(rows, cols);
        cofactors(i,j) = (-1)^(i+j) * ...
            (S(1,1)*S(2,2) - S(1,2)*S(2,1));
    end
end

d = 0;
for j = 1:3
    d = d + M(1,j)*cofactors(1,j);
end

Ainv = [];
if d ~= 0
    Ainv = cofactors.' / d;
end

A2 = zeros(size(A,1),size(A,2));
for i = 1:size(A,1)
    for j = 1:size(A,2)
        for k = 1:size(A,2)
            A2(i,j) = A2(i,j) + A(i,k)*A(k,j);
        end
    end
end

A3 = zeros(size(A2,1),size(A,2));
for i = 1:size(A2,1)
    for j = 1:size(A,2)
        for k = 1:size(A2,2)
            A3(i,j) = A3(i,j) + A2(i,k)*A(k,j);
        end
    end
end

A5 = zeros(size(A2,1),size(A3,2));
for i = 1:size(A2,1)
    for j = 1:size(A3,2)
        for k = 1:size(A2,2)
            A5(i,j) = A5(i,j) + A2(i,k)*A3(k,j);
        end
    end
end

AB = zeros(size(A,1),size(B,2));
for i = 1:size(A,1)
    for j = 1:size(B,2)
        for k = 1:size(A,2)
            AB(i,j) = AB(i,j) + A(i,k)*B(k,j);
        end
    end
end

AinvB = zeros(size(Ainv,1),size(B,2));
for i = 1:size(Ainv,1)
    for j = 1:size(B,2)
        for k = 1:size(Ainv,2)
            AinvB(i,j) = AinvB(i,j) + Ainv(i,k)*B(k,j);
        end
    end
end

A5B = zeros(size(A5,1),size(B,2));
for i = 1:size(A5,1)
    for j = 1:size(B,2)
        for k = 1:size(A5,2)
            A5B(i,j) = A5B(i,j) + A5(i,k)*B(k,j);
        end
    end
end

S = A2 + A3;

SB = zeros(size(S,1),size(B,2));
for i = 1:size(S,1)
    for j = 1:size(B,2)
        for k = 1:size(S,2)
            SB(i,j) = SB(i,j) + S(i,k)*B(k,j);
        end
    end
end

disp(A3)
disp(AB)
disp(AinvB)
disp(A5B)
disp(A + A2)
disp(SB)
```

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

disp(A^3)
disp(A*B)
disp(A\B)              % Computes A^(-1)*B by solving A*X = B
disp((A^5)*B)
disp(A + A^2)
disp((A^2 + A^3)*B)
```

#### Question 8 — Store the transpose of B in C

**Manual solution**

```matlab
B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

C = zeros(size(B,2),size(B,1));
for i = 1:size(B,1)
    for j = 1:size(B,2)
        C(j,i) = B(i,j);
    end
end

disp(C)
```

**Built-in solution**

```matlab
B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

C = B.';
disp(C)
```

#### Question 9 — Display the three indexed elements

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

C = B.';
disp([A(2,2), B(3,5), C(1,3)])   % [0 1 0]
```

#### Question 10 — Evaluate both matrix expressions

**Manual solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

I = zeros(3);
for i = 1:3
    I(i,i) = 1;
end
M = A;

cofactors = zeros(3);
for i = 1:3
    rows = [1:i-1 i+1:3];
    for j = 1:3
        cols = [1:j-1 j+1:3];
        S = M(rows, cols);
        cofactors(i,j) = (-1)^(i+j) * ...
            (S(1,1)*S(2,2) - S(1,2)*S(2,1));
    end
end

d = 0;
for j = 1:3
    d = d + M(1,j)*cofactors(1,j);
end

Ainv = [];
if d ~= 0
    Ainv = cofactors.' / d;
end

A2 = zeros(size(A,1),size(A,2));
for i = 1:size(A,1)
    for j = 1:size(A,2)
        for k = 1:size(A,2)
            A2(i,j) = A2(i,j) + A(i,k)*A(k,j);
        end
    end
end

AinvB = zeros(size(Ainv,1),size(B,2));
for i = 1:size(Ainv,1)
    for j = 1:size(B,2)
        for k = 1:size(Ainv,2)
            AinvB(i,j) = AinvB(i,j) + Ainv(i,k)*B(k,j);
        end
    end
end

C = zeros(size(B,2),size(B,1));
for i = 1:size(B,1)
    for j = 1:size(B,2)
        C(j,i) = B(i,j);
    end
end

CA = zeros(size(C,1),size(A,2));
for i = 1:size(C,1)
    for j = 1:size(A,2)
        for k = 1:size(C,2)
            CA(i,j) = CA(i,j) + C(i,k)*A(k,j);
        end
    end
end

CAt = zeros(size(CA,2),size(CA,1));
for i = 1:size(CA,1)
    for j = 1:size(CA,2)
        CAt(j,i) = CA(i,j);
    end
end

disp(I + A + A2)
disp(AinvB + CAt)
```

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];

B = [1 2 3 4 5; 0 1 0 1 0; 0 1 0 -1 1];

C = B.';
disp(eye(3) + A + A^2)
disp((A\B) + (C*A).')
```

### Matrix manipulation

#### Question 1 — Create the arrays

**Built-in solution**

```matlab
A = [1 2 3 4 5 6;
     2 3 4 5 6 7;
     3 4 5 6 7 8;
     4 5 6 7 8 9;
     5 6 7 8 9 10];
B = [2 4 6 8 10 12;
     6 8 10 12 14 16;
     10 12 14 16 18 20];
v = 9:-1:1;
```

#### Question 2 — Replace the requested elements in one command

The sheet gives three source entries for a four-entry destination in row 5. The first script fills columns 3–5 and keeps column 6. The second uses columns 3–6 of B if the intended replacement is four entries.

**Built-in solution**

```matlab
A = [1 2 3 4 5 6;
     2 3 4 5 6 7;
     3 4 5 6 7 8;
     4 5 6 7 8 9;
     5 6 7 8 9 10];
B = [2 4 6 8 10 12;
     6 8 10 12 14 16;
     10 12 14 16 18 20];
v = 9:-1:1;

A([1 3 4 5],3:6) = [B(1:2,1:4); v(5:8); B(3,3:5), A(5,6)];
disp(A)
```

**Built-in solution — alternative for four source entries**

```matlab
A = [1 2 3 4 5 6;
     2 3 4 5 6 7;
     3 4 5 6 7 8;
     4 5 6 7 8 9;
     5 6 7 8 9 10];
B = [2 4 6 8 10 12;
     6 8 10 12 14 16;
     10 12 14 16 18 20];
v = 9:-1:1;

A([1 3 4 5],3:6) = [B(1:2,1:4); v(5:8); B(3,3:6)];
disp(A)
```

## Labsheet 2

### Matrix multiplication

#### Question 1 — Row-by-column definition

**Manual solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];
B = [1 2 3 4; 0 1 0 1; 0 1 0 -1];

C = zeros(size(A,1),size(B,2));
for i = 1:size(A,1)
    for j = 1:size(B,2)
        for k = 1:size(A,2)
            C(i,j) = C(i,j) + A(i,k)*B(k,j);
        end
    end
end

disp(C)
```

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];
B = [1 2 3 4; 0 1 0 1; 0 1 0 -1];

C = zeros(size(A,1),size(B,2));
for i = 1:size(A,1)
    for j = 1:size(B,2)
        C(i,j) = dot(A(i,:),B(:,j).');
    end
end
disp(C)
```

#### Question 2 — Each output column as a linear combination of A's columns

**Manual solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];
B = [1 2 3 4; 0 1 0 1; 0 1 0 -1];

C = zeros(size(A,1),size(B,2));
for j = 1:size(B,2)
    for k = 1:size(A,2)
        C(:,j) = C(:,j) + B(k,j)*A(:,k);
    end
end
disp(C)
```

**Built-in solution**

```matlab
A = [1 2 1; -1 0 1; 1 1 -1];
B = [1 2 3 4; 0 1 0 1; 0 1 0 -1];

C = zeros(size(A,1),size(B,2));
for j = 1:size(B,2)
    C(:,j) = A*B(:,j);
end
disp(C)
```

### Linear span

#### Question 1 — Does (1, −3, 5) lie in the span?

**Manual solution**

```matlab
A = [1 1 4; 2 1 5; 1 -1 2];
w = [1; -3; 5];

E = double([A w]);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

inSpan = ~any(pivots == size(A,2)+1);
disp(inSpan)
if inSpan && r == size(A,2)
    disp(R(:,end))
end
```

**Built-in solution**

```matlab
S = [1 1 4; 2 1 5; 1 -1 2];
w = [1; -3; 5];
inSpan = rank(S) == rank([S w]);
disp(inSpan)            % true
if inSpan
    disp(S\w)           % [-7.5; -5.5; 3.5]
end
```

#### Question 2 — Find k so (2, 1, k) lies in the span

**Manual solution**

```matlab
% a + b = 2, 2*a = 1, k = 3*a - b
a = 1/2;
b = 2 - a;
k = 3*a - b;
disp(k)
```

**Built-in solution**

```matlab
S = [1 1; 2 0; 3 -1];
weights = S(1:2,:)\[2; 1];
k = S(3,:)*weights;
disp(k)                  % 0
```

#### Question 3 — Plot the span of u and v as a function

This question asks for a function. The full script includes a local function. The plot shows a finite patch of the plane.

**Built-in solution**

```matlab
plotSpan([1; 1; 1],[1; 2; 3])

function plotSpan(u,v)
    u = u(:);
    v = v(:);
    [a,b] = meshgrid(linspace(-2,2,31));
    X = a*u(1) + b*v(1);
    Y = a*u(2) + b*v(2);
    Z = a*u(3) + b*v(3);

    figure
    surf(X,Y,Z,'FaceAlpha',0.35,'EdgeColor','none');
    hold on
    quiver3(0,0,0,u(1),u(2),u(3),0,'r','LineWidth',2);
    quiver3(0,0,0,v(1),v(2),v(3),0,'b','LineWidth',2);
    axis equal
    grid on
    xlabel('x'); ylabel('y'); zlabel('z');
    title('Span of u and v')
    legend('Span patch','u','v','Location','best')
    view(3)
end
```

### Linear dependence and independence

#### Question 1 — Plot u, v, w and inspect their geometry

**Built-in solution**

```matlab
u = [1; 1; 1]; v = [1; 0; 1]; w = [2; 2; 2];
figure
hold on
quiver3(0,0,0,w(1),w(2),w(3),0,'k','LineWidth',2);
quiver3(0,0,0,u(1),u(2),u(3),0,'r','LineWidth',2);
quiver3(0,0,0,v(1),v(2),v(3),0,'b','LineWidth',2);
axis equal
grid on
xlabel('x'); ylabel('y'); zlabel('z');
legend('w','u','v','Location','best')
title('u and w point along the same line')
view(3)
disp(all(w == 2*u))   % true: w = 2*u, so the set is dependent
```

#### Question 2 — Check independence of the three given vectors

**Manual solution**

```matlab
M = [1 0 -1; 2 3 0; 0 1 1];
d = M(1,1)*(M(2,2)*M(3,3)-M(2,3)*M(3,2)) ...
    - M(1,2)*(M(2,1)*M(3,3)-M(2,3)*M(3,1)) ...
    + M(1,3)*(M(2,1)*M(3,2)-M(2,2)*M(3,1));
disp(d)
disp(d ~= 0)
```

**Built-in solution**

```matlab
M = [1 0 -1; 2 3 0; 0 1 1];
disp(rank(M) == size(M,2))   % true
```

#### Question 3 — Find all k for which the vectors are independent

**Manual solution**

```matlab
% det(M) = 1*(k*k - 1*0) - 1*(0*k - 1*k)
%        = k^2 + k = k*(k + 1).
excluded = [-1 0];
disp(excluded)
disp('Independent for every real k except -1 and 0.')
```

**Built-in solution (Symbolic Math Toolbox)**

```matlab
syms k real
M = [1 1 0; 0 k 1; k 0 k];
disp(factor(det(M)))
disp(solve(det(M) == 0,k))   % Excluded values: -1 and 0
```

## Labsheet 3

### Basis of a vector space

#### Question 1 — Show that B forms a basis of R³

**Manual solution**

```matlab
B = [1 1 4; 2 1 5; 1 -1 2];

M = B;
d = M(1,1)*(M(2,2)*M(3,3)-M(2,3)*M(3,2)) ...
    - M(1,2)*(M(2,1)*M(3,3)-M(2,3)*M(3,1)) ...
    + M(1,3)*(M(2,1)*M(3,2)-M(2,2)*M(3,1));
disp(d)
disp(d ~= 0)
```

**Built-in solution**

```matlab
B = [1 1 4; 2 1 5; 1 -1 2];

r = rank(B);
disp(r)          % 3
disp(r == 3)     % Three independent columns span R^3
```

#### Question 2 — Coordinate vector of (1, −3, 5) relative to B

**Manual solution**

```matlab
B = [1 1 4; 2 1 5; 1 -1 2];
w = [1; -3; 5];

E = double([B w]);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

coordinates = R(:,end);
disp(coordinates)
```

**Built-in solution**

```matlab
B = [1 1 4; 2 1 5; 1 -1 2];
w = [1; -3; 5];

coordinates = B\w;
disp(coordinates)   % [-7.5; -5.5; 3.5]
```

### Echelon forms

#### Question 3 — Return REF, RREF, and rank

This question asks for a function. Each script includes its own local function. Expected rank: 2. The matrix is rank deficient.

**Manual solution**

```matlab
A = [1 3 1 -2 -3; 1 4 3 -1 -4;
     2 3 -4 -7 -3; 3 8 1 -7 -8];
[E,R,r] = echelonForms(A);
disp(E)
disp(R)
disp(r)
disp(r < min(size(A)))

function [E,R,r,pivots] = echelonForms(A)
    E = double(A);
    [m,n] = size(E);
    scale = max([1; abs(E(:))]);
    tol = max(m,n)*eps(scale);
    pivots = zeros(1,min(m,n));
    r = 0;

    for col = 1:n
        if r == m
            break
        end
        row = r+1;
        [pivotSize,offset] = max(abs(E(row:m,col)));
        if pivotSize <= tol
            E(row:m,col) = 0;
            continue
        end

        pivotRow = row+offset-1;
        E([row pivotRow],:) = E([pivotRow row],:);
        for i = row+1:m
            factor = E(i,col)/E(row,col);
            E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
            E(i,col) = 0;
        end
        r = row;
        pivots(r) = col;
    end

    pivots = pivots(1:r);
    R = E;
    for row = r:-1:1
        col = pivots(row);
        R(row,:) = R(row,:)/R(row,col);
        for i = 1:row-1
            R(i,:) = R(i,:) - R(i,col)*R(row,:);
            R(i,col) = 0;
        end
    end
end
```

**Built-in solution**

```matlab
A = [1 3 1 -2 -3; 1 4 3 -1 -4;
     2 3 -4 -7 -3; 3 8 1 -7 -8];
[E,R,r] = echelonForms(A);
disp(E)
disp(R)
disp(r)
disp(r < min(size(A)))

function [E,R,r] = echelonForms(A)
    [R,pivots] = rref(A);
    r = numel(pivots);
    [~,U,~] = lu(A);
    tol = max(size(A))*eps(max(1,norm(A,inf)));
    U(abs(U) <= tol) = 0;
    [hasLeading,leading] = max(U ~= 0,[],2);
    E = U(logical(hasLeading),:);
    leading = leading(logical(hasLeading));
    [leading,order] = sort(leading);
    E = E(order,:);
    if numel(leading) == r && all(diff(leading) > 0)
        E = [E; zeros(size(A,1)-size(E,1),size(A,2))];
    else
        E = R;    % Every reduced echelon form is also an echelon form
    end
end
```

#### Question 4 — Check consistency and solve the system both ways

**Manual solution**

```matlab
A = [1 5 -1; 1 0 1; 3 5 0];
b = [0; 4; 6];

E = double([A b]);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

n = size(A,2);
if ~any(pivots == n+1)
    disp('Consistent')
    xGauss = zeros(n,1);
    for i = n:-1:1
        remainder = E(i,end);
        for j = i+1:n
            remainder = remainder - E(i,j)*xGauss(j);
        end
        xGauss(i) = remainder/E(i,i);
    end
    xGaussJordan = R(:,end);
    disp(xGauss)
    disp(xGaussJordan)
else
    disp('Inconsistent')
end
```

**Built-in solution**

```matlab
A = [1 5 -1; 1 0 1; 3 5 0];
b = [0; 4; 6];
n = size(A,2);

if rank(A) == rank([A b])
    disp('Consistent')
    [L,U,P] = lu(A);
    xGauss = U\(L\(P*b));
    R = rref([A b]);
    xGaussJordan = R(:,end);
    disp(xGauss)
    disp(xGaussJordan)
else
    disp('Inconsistent')
end
```

### Subspaces associated with a matrix

#### Question 5 — Bases and dimensions of the column space and null space

**Manual solution**

```matlab
A = [1 2 -2 2 -1; 0 0 1 2 4; 0 0 0 1 -2; 0 0 0 0 0];

E = double(A);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

n = size(A,2);
isFree = true(1,n);
isFree(pivots) = false;
free = find(isFree);
columnBasis = A(:,pivots);
nullBasis = zeros(n,numel(free));
for j = 1:numel(free)
    col = free(j);
    nullBasis(col,j) = 1;
    nullBasis(pivots,j) = -R(1:r,col);
end

disp(columnBasis)
disp(r)
disp(nullBasis)
disp(size(nullBasis,2))
```

**Built-in solution**

```matlab
A = [1 2 -2 2 -1; 0 0 1 2 4; 0 0 0 1 -2; 0 0 0 0 0];
[~,pivots] = rref(A);
columnBasis = A(:,pivots);
nullBasis = null(A);
disp(columnBasis)
disp(size(columnBasis,2))   % 3
disp(nullBasis)
disp(size(nullBasis,2))     % 2
```

#### Question 6 — Verify the rank–nullity theorem

**Manual solution**

```matlab
A = [1 1 1; 1 2 3; 1 3 6];

E = double(A);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

n = size(A,2);
isFree = true(1,n);
isFree(pivots) = false;
free = find(isFree);
columnBasis = A(:,pivots);
nullBasis = zeros(n,numel(free));
for j = 1:numel(free)
    col = free(j);
    nullBasis(col,j) = 1;
    nullBasis(pivots,j) = -R(1:r,col);
end

nullity = size(nullBasis,2);
disp([r nullity n])
assert(r + nullity == n)
```

**Built-in solution**

```matlab
A = [1 1 1; 1 2 3; 1 3 6];
r = rank(A);
nullity = size(null(A),2);
n = size(A,2);
disp([r nullity n])        % [3 0 3]
assert(r + nullity == n)
```

#### Question 7 — Basis and dimension of the homogeneous solution space

The last equation uses `8z`. The scripts interpret it as `8c` to match the variables `a,b,c,d`.

**Manual solution**

```matlab
A = [1 2 2 3; 1 2 3 1; 3 6 8 5];

E = double(A);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

n = size(A,2);
isFree = true(1,n);
isFree(pivots) = false;
free = find(isFree);
columnBasis = A(:,pivots);
nullBasis = zeros(n,numel(free));
for j = 1:numel(free)
    col = free(j);
    nullBasis(col,j) = 1;
    nullBasis(pivots,j) = -R(1:r,col);
end

disp(nullBasis)
disp(size(nullBasis,2))
```

**Built-in solution**

```matlab
A = [1 2 2 3; 1 2 3 1; 3 6 8 5];
N = null(A);
disp(N)
disp(size(N,2))    % 2
```

## Labsheet 4

#### Question 1 — Standard matrix of T and T(2, −1)

The stated codomain is R³. The scripts assume the plus sign before `3x − y` was intended as a comma.

**Manual solution**

```matlab
e1 = [1; 0];
e2 = [0; 1];
A = zeros(3,2);
inputBasis = [e1 e2];
for j = 1:2
    x = inputBasis(1,j);
    y = inputBasis(2,j);
    A(:,j) = [x+2*y; 2*x-y; 3*x-y];
end
disp(A)
disp(2*A(:,1) - A(:,2))
```

**Built-in solution (Symbolic Math Toolbox)**

```matlab
syms x y real
T = [x+2*y; 2*x-y; 3*x-y];
A = jacobian(T,[x y]);
disp(A)
disp(A*[2; -1])    % [0; 5; 7]
```

#### Question 2 — Angle between u and v

Use the corrected formula `cos(theta) = dot(u,v)/(norm(u)*norm(v))`. The angle is approximately 62.19°.

**Manual solution**

```matlab
u = [1; 2; 3]; v = [4; -1; 2];

p = 0;
sumU = 0;
sumV = 0;
for i = 1:numel(u)
    p = p + u(i)*v(i);
    sumU = sumU + u(i)^2;
    sumV = sumV + v(i)^2;
end
nu = sqrt(sumU);
nv = sqrt(sumV);
if nu == 0 || nv == 0
    thetaDeg = NaN;
else
    c = p/(nu*nv);
    thetaDeg = acos(max(-1,min(1,c)))*180/pi;
end

disp(thetaDeg)
```

**Built-in solution**

```matlab
u = [1; 2; 3]; v = [4; -1; 2];
cosTheta = dot(u,v)/(norm(u)*norm(v));
thetaDeg = acosd(max(-1,min(1,cosTheta)));
disp(thetaDeg)
```

#### Question 3 — Pairwise inner products, norms, and angles

Rows of `pairResults` correspond to (u,v), (u,w), and (v,w). Columns are the inner product and angle in degrees.

**Manual solution**

```matlab
V = [1 2 1; 2 -1 1; -1 0 3];
norms = zeros(1,3);
for j = 1:3
    squaredLength = 0;
    for i = 1:3
        squaredLength = squaredLength + V(i,j)^2;
    end
    norms(j) = sqrt(squaredLength);
end
pairs = [1 2; 1 3; 2 3];
pairResults = zeros(3,2);
for k = 1:3
    i = pairs(k,1);
    j = pairs(k,2);
    innerProduct = 0;
    for component = 1:3
        innerProduct = innerProduct + V(component,i)*V(component,j);
    end
    c = innerProduct/(norms(i)*norms(j));
    pairResults(k,:) = [innerProduct, acos(max(-1,min(1,c)))*180/pi];
end
disp(norms)
disp(pairResults)
```

**Built-in solution**

```matlab
V = [1 2 1; 2 -1 1; -1 0 3];   % Columns: u, v, w
norms = vecnorm(V);
pairs = [1 2; 1 3; 2 3];
pairResults = zeros(3,2);
for k = 1:3
    i = pairs(k,1);
    j = pairs(k,2);
    p = dot(V(:,i),V(:,j));
    c = p/(norms(i)*norms(j));
    pairResults(k,:) = [p, acosd(max(-1,min(1,c)))];
end
disp(norms)
disp(pairResults)
```

#### Question 4 — Image, range, kernel, rank, nullity, and angle

Expected image: `[8;16;6]`. Rank is 2 and nullity is 1.

**Manual solution**

```matlab
A = [1 2 1; 2 4 2; 1 1 1];
x = [1; 2; 3];
u = [1; 0; 1]; v = [0; 1; 1];

E = double(A);
[m,n] = size(E);
scale = max([1; abs(E(:))]);
tol = max(m,n)*eps(scale);
pivots = zeros(1,min(m,n));
r = 0;

for col = 1:n
    if r == m
        break
    end
    row = r+1;
    [pivotSize,offset] = max(abs(E(row:m,col)));
    if pivotSize <= tol
        E(row:m,col) = 0;
        continue
    end

    pivotRow = row+offset-1;
    E([row pivotRow],:) = E([pivotRow row],:);
    for i = row+1:m
        factor = E(i,col)/E(row,col);
        E(i,col:n) = E(i,col:n) - factor*E(row,col:n);
        E(i,col) = 0;
    end
    r = row;
    pivots(r) = col;
end

pivots = pivots(1:r);
R = E;
for row = r:-1:1
    col = pivots(row);
    R(row,:) = R(row,:)/R(row,col);
    for i = 1:row-1
        R(i,:) = R(i,:) - R(i,col)*R(row,:);
        R(i,col) = 0;
    end
end

n = size(A,2);
isFree = true(1,n);
isFree(pivots) = false;
free = find(isFree);
columnBasis = A(:,pivots);
nullBasis = zeros(n,numel(free));
for j = 1:numel(free)
    col = free(j);
    nullBasis(col,j) = 1;
    nullBasis(pivots,j) = -R(1:r,col);
end

rangeBasis = columnBasis;
kernelBasis = nullBasis;
nullity = size(kernelBasis,2);
verified = r + nullity == size(A,2);

inputs = [x u v];

images = zeros(size(A,1),size(inputs,2));
for i = 1:size(A,1)
    for j = 1:size(inputs,2)
        for k = 1:size(A,2)
            images(i,j) = images(i,j) + A(i,k)*inputs(k,j);
        end
    end
end

Tx = images(:,1);
Tu = images(:,2);
Tv = images(:,3);

p = 0;
sumU = 0;
sumV = 0;
for i = 1:numel(Tu)
    p = p + Tu(i)*Tv(i);
    sumU = sumU + Tu(i)^2;
    sumV = sumV + Tv(i)^2;
end
nu = sqrt(sumU);
nv = sqrt(sumV);
if nu == 0 || nv == 0
    thetaDeg = NaN;
else
    c = p/(nu*nv);
    thetaDeg = acos(max(-1,min(1,c)))*180/pi;
end

disp(Tx)
disp(rangeBasis)
disp(kernelBasis)
disp([r nullity])
disp(verified)
disp(thetaDeg)
```

**Built-in solution**

```matlab
A = [1 2 1; 2 4 2; 1 1 1];
x = [1; 2; 3];
u = [1; 0; 1]; v = [0; 1; 1];

Tx = A*x;                                 % (i)
[~,pivots] = rref(A);
rangeBasis = A(:,pivots);                 % (ii)
kernelBasis = null(A);                    % (iii)
r = rank(A);                             % (iv)
nullity = size(kernelBasis,2);            % (v)
verified = r + nullity == size(A,2);       % (vi)

Tu = A*u; Tv = A*v;
c = dot(Tu,Tv)/(norm(Tu)*norm(Tv));
thetaDeg = acosd(max(-1,min(1,c)));        % (vii)

disp(Tx)
disp(rangeBasis)
disp(kernelBasis)
disp([r nullity])
disp(verified)
disp(thetaDeg)
```

## Labsheet 5

### Gram–Schmidt orthogonalisation and QR decomposition

#### Question 1 — Test whether the given vectors form an orthonormal set

**Manual solution**

```matlab
A = [1/sqrt(2), 1/sqrt(2), 0; 1/sqrt(2), -1/sqrt(2), 0; 0, 0, 1];

G = zeros(3);
for i = 1:3
    for j = 1:3
        for k = 1:3
            G(i,j) = G(i,j) + A(k,i)*A(k,j);
        end
    end
end
disp(G)
disp(max(abs(G(:) - reshape(eye(3),[],1))) < 1e-12)
```

**Built-in solution**

```matlab
A = [1/sqrt(2), 1/sqrt(2), 0; 1/sqrt(2), -1/sqrt(2), 0; 0, 0, 1];

G = A.'*A;
disp(G)
disp(norm(G - eye(3),'fro') < 1e-12)
```

#### Question 2 — Convert the given vectors into orthonormal vectors

**Manual solution**

```matlab
A = [1 3; 2 -1];

[m,n] = size(A);
Q = zeros(m,n);
R = zeros(n);
for j = 1:n
    v = A(:,j);
    for i = 1:j-1
        R(i,j) = Q(:,i).'*v;
        v = v - R(i,j)*Q(:,i);
    end
    R(j,j) = sqrt(sum(v.^2));
    Q(:,j) = v/R(j,j);
end

disp(Q)
disp(Q.'*Q)
```

**Built-in solution**

```matlab
A = [1 3; 2 -1];

[Q,R] = qr(A,0);

disp(Q)
disp(Q.'*Q)
```

#### Question 3 — Convert the given vectors into orthonormal vectors

**Manual solution**

```matlab
A = [1 2 1; 2 -1 1; -1 0 3];

[m,n] = size(A);
Q = zeros(m,n);
R = zeros(n);
for j = 1:n
    v = A(:,j);
    for i = 1:j-1
        R(i,j) = Q(:,i).'*v;
        v = v - R(i,j)*Q(:,i);
    end
    R(j,j) = sqrt(sum(v.^2));
    Q(:,j) = v/R(j,j);
end

disp(Q)
disp(Q.'*Q)
```

**Built-in solution**

```matlab
A = [1 2 1; 2 -1 1; -1 0 3];

[Q,R] = qr(A,0);

disp(Q)
disp(Q.'*Q)
```

#### Question 4 — Find the QR decomposition using Gram–Schmidt

**Manual solution**

```matlab
A = [1 2 1; 2 4 6; 1 1 1];

[m,n] = size(A);
Q = zeros(m,n);
R = zeros(n);
for j = 1:n
    v = A(:,j);
    for i = 1:j-1
        R(i,j) = Q(:,i).'*v;
        v = v - R(i,j)*Q(:,i);
    end
    R(j,j) = sqrt(sum(v.^2));
    Q(:,j) = v/R(j,j);
end

disp(Q)
disp(R)
disp(norm(A-Q*R,'fro'))
```

**Built-in solution**

```matlab
A = [1 2 1; 2 4 6; 1 1 1];

[Q,R] = qr(A,0);

disp(Q)
disp(R)
disp(norm(A-Q*R,'fro'))
```

## Labsheet 6

### Singular value decomposition and low-rank approximation

#### Question 1 — Compute the SVD and verify reconstruction

The manual version builds the SVD from the eigendecomposition of the Gram matrix. The displayed error should be close to zero.

**Manual solution**

```matlab
A = [3 1 1; -1 3 1];

[V,D] = eig(A.'*A);
[lambda,order] = sort(diag(D),'descend');
V = V(:,order);

sigma = sqrt(lambda(1:2));
U = zeros(2);
S = zeros(2,3);
for j = 1:2
    U(:,j) = A*V(:,j)/sigma(j);
    S(j,j) = sigma(j);
end

disp(U)
disp(S)
disp(V)
disp(norm(A - U*S*V.','fro'))
```

**Built-in solution**

```matlab
A = [3 1 1; -1 3 1];

[U,S,V] = svd(A);

disp(U)
disp(S)
disp(V)
disp(norm(A - U*S*V.','fro'))
```

#### Question 2 — Compute the SVD and construct the rank-1 approximation

The matrix is already rank 1. The manual version factors it as an outer product and uses reflections to complete the singular-vector bases.

**Manual solution**

```matlab
A = [1 2 3; 2 4 6; 3 6 9; 4 8 12];

p = A(:,1);
v = A(1,:).'/p(1);
np = sqrt(sum(p.^2));
nv = sqrt(sum(v.^2));
u1 = p/np;
v1 = v/nv;

% Reflect e1 onto each leading singular vector.
eU = [1; 0; 0; 0];
eV = [1; 0; 0];
wU = eU - u1;
wV = eV - v1;
U = eye(4) - 2*(wU*wU.')/(wU.'*wU);
V = eye(3) - 2*(wV*wV.')/(wV.'*wV);
S = zeros(4,3);
S(1,1) = np*nv;

A1 = S(1,1)*U(:,1)*V(:,1).';
disp(U)
disp(S)
disp(V)
disp(A1)
disp(norm(A-A1,'fro'))
```

**Built-in solution**

```matlab
A = [1 2 3; 2 4 6; 3 6 9; 4 8 12];

[U,S,V] = svd(A);

A1 = S(1,1)*U(:,1)*V(:,1).';
disp(U)
disp(S)
disp(V)
disp(A1)
disp(norm(A-A1,'fro'))
```

#### Question 3 — Compare rank-1 and rank-2 approximations

The matrix has rank 2. The rank-2 approximation reconstructs it up to rounding error.

**Manual solution**

```matlab
A = [1 2 3; 4 5 6; 7 8 9; 10 11 12];

[V,D] = eig(A.'*A);
[lambda,order] = sort(diag(D),'descend');
V = V(:,order);

% sigma_j*u_j = A*v_j, so each term is (A*v_j)*v_j'.
v1 = V(:,1);
v2 = V(:,2);
A1 = (A*v1)*v1.';
A2 = A1 + (A*v2)*v2.';

disp(A1)
disp(A2)
error1 = norm(A-A1,'fro');
error2 = norm(A-A2,'fro');
fprintf('Rank-1 error: %.8g\nRank-2 error: %.8g\n',error1,error2);
```

**Built-in solution**

```matlab
A = [1 2 3; 4 5 6; 7 8 9; 10 11 12];

[U,S,V] = svd(A,'econ');
A1 = U(:,1)*S(1,1)*V(:,1).';
A2 = U(:,1:2)*S(1:2,1:2)*V(:,1:2).';

disp(A1)
disp(A2)
error1 = norm(A-A1,'fro');
error2 = norm(A-A2,'fro');
fprintf('Rank-1 error: %.8g\nRank-2 error: %.8g\n',error1,error2);
```

## Labsheet 7

### PCA and dimensionality reduction

#### Question 1 — Perform PCA on the 2D data and plot the 1D scores

Only PC1 has nonzero variance. The sign of a principal component and its scores may flip between versions.

**Manual solution**

```matlab
X = [(2:9).' (1:8).'];

n = size(X,1);
Xc = X - sum(X,1)/n;
C = (Xc.'*Xc)/(n-1);
[V,D] = eig(C);
[latent,idx] = sort(diag(D),'descend');
coeff = V(:,idx);

disp(Xc)
disp(C)
scores = Xc*coeff(:,1);

disp(coeff)
disp(latent)
disp(scores)

figure
subplot(1,2,1)
scatter(X(:,1),X(:,2),40,'filled')
xlabel('Feature 1')
ylabel('Feature 2')
title('Original data')
grid on
subplot(1,2,2)
scatter(scores,zeros(size(scores)),40,'filled')
xlabel('PC1 score')
yticks([])
title('One-dimensional projection')
grid on
```

**Built-in solution (Statistics and Machine Learning Toolbox)**

```matlab
X = [(2:9).' (1:8).'];

[coeff,score,latent] = pca(X);
scores = score(:,1);

disp(coeff)
disp(latent)
disp(scores)

figure
subplot(1,2,1)
scatter(X(:,1),X(:,2),40,'filled')
xlabel('Feature 1')
ylabel('Feature 2')
title('Original data')
grid on
subplot(1,2,2)
scatter(scores,zeros(size(scores)),40,'filled')
xlabel('PC1 score')
yticks([])
title('One-dimensional projection')
grid on
```

#### Question 2 — Add two features and reduce from 4D to 3D

The three output columns are PC scores. Only PC1 has nonzero variance because all four centered features are identical.

**Manual solution**

```matlab
X = [(2:9).' (1:8).' (3:10).' (0:7).'];

n = size(X,1);
Xc = X - sum(X,1)/n;
C = (Xc.'*Xc)/(n-1);
[V,D] = eig(C);
[latent,idx] = sort(diag(D),'descend');
coeff = V(:,idx);

scores = Xc*coeff(:,1:3);

disp(coeff(:,1:3))
disp(latent)
disp(scores)
```

**Built-in solution (Statistics and Machine Learning Toolbox)**

```matlab
X = [(2:9).' (1:8).' (3:10).' (0:7).'];

[coeff,score,latent] = pca(X);
scores = score(:,1:3);

disp(coeff(:,1:3))
disp(latent)
disp(scores)
```

## Labsheet 8

### Householder matrices and transformations

#### Question 1 — Construct a Householder matrix for the first column

This sign convention maps the first column to approximately `[-5; 0; 0]`.

**Manual solution**

```matlab
A = [4 1; 3 2; 0 5];

x = A(:,1);
alpha = -sqrt(sum(x.^2));
v = x - [alpha; 0; 0];
H = eye(3) - 2*(v*v.')/(v.'*v);
disp(H)
disp(H*x)
```

#### Question 2 — Obtain QR decompositions using Householder transformations

Each part has a separate script. QR factors can differ in sign. Part (iii) is rank deficient, so a diagonal entry of R is numerically zero.

##### Part (i)

**Manual solution**

```matlab
A = [1 1; 1 0; 0 1];

[m,n] = size(A);
Q = eye(m);
R = A;
tol = 1e-12*norm(A,'fro');
for k = 1:min(m-1,n)
    x = R(k:m,k);
    if norm(x(2:end)) <= tol
        continue
    end
    alpha = -sqrt(sum(x.^2));
    if x(1) < 0
        alpha = -alpha;
    end
    v = x;
    v(1) = v(1) - alpha;
    H = eye(m);
    H(k:m,k:m) = eye(m-k+1) - 2*(v*v.')/(v.'*v);
    R = H*R;
    Q = Q*H;
end

disp(Q)
disp(R)
disp(norm(Q*R-A,'fro'))
disp(norm(Q.'*Q-eye(size(Q,2)),'fro'))
```

**Built-in solution**

```matlab
A = [1 1; 1 0; 0 1];

[Q,R] = qr(A);

disp(Q)
disp(R)
disp(norm(Q*R-A,'fro'))
disp(norm(Q.'*Q-eye(size(Q,2)),'fro'))
```

##### Part (ii)

**Manual solution**

```matlab
A = [3 2 1 -1; 1 3 1 -1; 4 1 3 1; -1 1 1 3];

[m,n] = size(A);
Q = eye(m);
R = A;
tol = 1e-12*norm(A,'fro');
for k = 1:min(m-1,n)
    x = R(k:m,k);
    if norm(x(2:end)) <= tol
        continue
    end
    alpha = -sqrt(sum(x.^2));
    if x(1) < 0
        alpha = -alpha;
    end
    v = x;
    v(1) = v(1) - alpha;
    H = eye(m);
    H(k:m,k:m) = eye(m-k+1) - 2*(v*v.')/(v.'*v);
    R = H*R;
    Q = Q*H;
end

disp(Q)
disp(R)
disp(norm(Q*R-A,'fro'))
disp(norm(Q.'*Q-eye(size(Q,2)),'fro'))
```

**Built-in solution**

```matlab
A = [3 2 1 -1; 1 3 1 -1; 4 1 3 1; -1 1 1 3];

[Q,R] = qr(A);

disp(Q)
disp(R)
disp(norm(Q*R-A,'fro'))
disp(norm(Q.'*Q-eye(size(Q,2)),'fro'))
```

##### Part (iii)

**Manual solution**

```matlab
A = [1 0 1 0; 0 1 0 1; -1 0 1 0; 0 1 0 1];

[m,n] = size(A);
Q = eye(m);
R = A;
tol = 1e-12*norm(A,'fro');
for k = 1:min(m-1,n)
    x = R(k:m,k);
    if norm(x(2:end)) <= tol
        continue
    end
    alpha = -sqrt(sum(x.^2));
    if x(1) < 0
        alpha = -alpha;
    end
    v = x;
    v(1) = v(1) - alpha;
    H = eye(m);
    H(k:m,k:m) = eye(m-k+1) - 2*(v*v.')/(v.'*v);
    R = H*R;
    Q = Q*H;
end

disp(Q)
disp(R)
disp(norm(Q*R-A,'fro'))
disp(norm(Q.'*Q-eye(size(Q,2)),'fro'))
```

**Built-in solution**

```matlab
A = [1 0 1 0; 0 1 0 1; -1 0 1 0; 0 1 0 1];

[Q,R] = qr(A);

disp(Q)
disp(R)
disp(norm(Q*R-A,'fro'))
disp(norm(Q.'*Q-eye(size(Q,2)),'fro'))
```

## Labsheet 9

### PageRank and spectral clustering

#### Question 1 — Construct the webpage adjacency matrix and compute PageRank

Rows are source pages and columns are destinations. Both scripts use a damping factor of 0.85 and uniform teleportation. Expected ranking: Page 3 > Page 2 > Page 1 > Page 4.

**Manual solution**

```matlab
A = [0 1 1 0; 0 0 1 0; 1 1 0 0; 0 1 1 0];

n = size(A,1);
d = 0.85;
P = A./sum(A,2);

scores = ones(n,1)/n;
for step = 1:1000
    updated = d*P.'*scores + (1-d)/n*ones(n,1);
    if sum(abs(updated-scores)) < 1e-12
        scores = updated;
        break
    end
    scores = updated;
end

[sortedScores,order] = sort(scores,'descend');
disp(A)
disp(table(order,sortedScores,'VariableNames',{'Page','PageRank'}))
```

**Built-in solution**

```matlab
A = [0 1 1 0; 0 0 1 0; 1 1 0 0; 0 1 1 0];

n = size(A,1);
d = 0.85;
P = A./sum(A,2);

scores = (eye(n) - d*P.') \ ((1-d)/n*ones(n,1));

[sortedScores,order] = sort(scores,'descend');
disp(A)
disp(table(order,sortedScores,'VariableNames',{'Page','PageRank'}))
```

#### Question 2 — Use the Fiedler vector to partition the ten-node graph

Both scripts use `eig` for the eigendecomposition, as requested by the sheet. The manual version builds the adjacency and degree matrices directly. The sign of the Fiedler vector can swap the cluster labels. The partition is {1, 2, 3, 4, 5} and {6, 7, 8, 9, 10}, with second-smallest eigenvalue approximately 0.96063.

**Manual solution**

```matlab
edges = [1 2; 1 3; 1 6; 1 7; 2 4; 2 5; 3 5; 4 5; 5 7; 5 9;
         6 7; 6 8; 7 8; 7 9; 7 10; 8 9; 8 10; 9 10];
n = 10;

A = zeros(n);
for k = 1:size(edges,1)
    i = edges(k,1);
    j = edges(k,2);
    A(i,j) = 1;
    A(j,i) = 1;
end
D = zeros(n);
for i = 1:n
    D(i,i) = sum(A(i,:));
end
L = D - A;

[V,E] = eig(full(L));
[eigenvalues,idx] = sort(diag(E),'ascend');
V = V(:,idx);
fiedler = V(:,2);
cluster1 = find(fiedler >= 0);
cluster2 = find(fiedler < 0);
disp(A)
disp(D)
disp(L)
disp(eigenvalues)
disp(V)
disp(fiedler)
disp(cluster1.')
disp(cluster2.')

x = [1 0 2 0 2 5 4 6 4 6];
y = [2 1 1 0 0 2 1 1 0 0];

figure
hold on
for k = 1:size(edges,1)
    nodes = edges(k,:);
    plot(x(nodes),y(nodes),'Color',[0.55 0.55 0.55])
end
scatter(x(cluster1),y(cluster1),90,'b','filled')
scatter(x(cluster2),y(cluster2),90,'r','filled')
for i = 1:n
    text(x(i),y(i)+0.16,num2str(i),'HorizontalAlignment','center')
end
axis equal
xlim([-0.5 6.5])
ylim([-0.4 2.5])
axis off
title('Spectral clustering by Fiedler vector sign')
```

**Built-in solution**

```matlab
edges = [1 2; 1 3; 1 6; 1 7; 2 4; 2 5; 3 5; 4 5; 5 7; 5 9;
         6 7; 6 8; 7 8; 7 9; 7 10; 8 9; 8 10; 9 10];
n = 10;

G = graph(edges(:,1),edges(:,2),[],n);
A = full(adjacency(G));
D = diag(degree(G));
L = laplacian(G);

[V,E] = eig(full(L));
[eigenvalues,idx] = sort(diag(E),'ascend');
V = V(:,idx);
fiedler = V(:,2);
cluster1 = find(fiedler >= 0);
cluster2 = find(fiedler < 0);
disp(A)
disp(D)
disp(L)
disp(eigenvalues)
disp(V)
disp(fiedler)
disp(cluster1.')
disp(cluster2.')

x = [1 0 2 0 2 5 4 6 4 6];
y = [2 1 1 0 0 2 1 1 0 0];

figure
p = plot(G,'XData',x,'YData',y,'MarkerSize',8);
highlight(p,cluster1,'NodeColor','b')
highlight(p,cluster2,'NodeColor','r')
axis equal
axis off
title('Spectral clustering by Fiedler vector sign')
```
