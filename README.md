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
