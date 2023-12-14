# Differentiation<br>

**개요**<br>
* [gradient1D( )]()<br>
* [acceleration( )]()<br>


<hr>

## gradient1D( )<br>

```c
void gradient1D(double x[], double y[], double dydx[], int m);
```
>Parameter<br>
**x[]** : x data set <br>
**y[]** : y data set <br>
**dydx[]** : 미분 값을 저장한 배열 선언 <br>

1. myNP.h 안에 선언되어 있다.
2. 다음과 같은 원리를 기반으로 작성되었다.<br>

* The truncation error can be estimated using Taylor sereies.

$$f(x)=\sum_{k=0}^nf^{(k)}(x_0){{x-x_0}^k\over{k!}}+E_{n+1}$$

* Two point forward difference

$$f^{'}(x_i)={{f(x_{i+1})-f(x_i)}\over h}$$
$$Truncation Error:O(h)$$

* Two point backward difference

$$f^{'}(x_i)={{f(x_{i})-f(x_{i-1})}\over h}$$
$$Truncation Error:O(h)$$

* Two point central difference

$$f^{'}(x_i)={{f(x_{i+1})-f(x_{i-1})}\over 2h}$$
$$Truncation Error:O(h^2)$$

* Three point forward difference

$$f^{'}(x_i)={{-3f(x_{i})+4f(x_{i+1})-f(x_{i+2})}\over 2h}$$
$$Truncation Error:O(h^2)$$

* Three point backward difference

$$f^{'}(x_i)={{3f(x_{i})-4f(x_{i-1})+f(x_{i-2})}\over 2h}$$
$$Truncation Error:O(h^2)$$

* Four point central difference

$$f^{'}(x_i)={{f(x_{i-2})-8f(x_{i-1})+8f(x_{i+1})-f(x_{i+2})}\over 12h}$$
$$Truncation Error:O(h^4)$$
    


<hr>

## Example <br>
```c++
int main()
{
    int m = 12;
    double X[] = { -1, -0.5, 0, 0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4, 4.5 };

    double Y[] = { -3.632, -0.3935, 1, 0.6487, -1.282, -4.518, -8.611,-12.82,-15.91,-15.88,-9.402,9.017 };
    double  dYdX[12] = { 0 };

    gradient1D(X, Y, dYdX, m);
    printVec(dYdX, m);
}
```

## Output <br>
```c
Vector[0] = 4.16
Vector[1] = 2.32
Vector[2] = 0.52
Vector[3] = -1.14
Vector[4] = -2.58
Vector[5] = -3.66
Vector[6] = -4.15
Vector[7] = -3.65
Vector[8] = -1.53
Vector[9] = 3.25
Vector[10] = 12.45
Vector[11] = 24.39
```

## Warning
>The length of x and y must be equal<br>
The length of data must be more than 2

## Error Handling
```c
if (sizeof(x) != sizeof(y)) {
	printf("ERROR: length of x and y must be equal\n");
	return;
}

if (m < 3) {
	printf("ERROR: length of data must be more than 2\n");
	return;
}
```
<br>

## acceleration( )<br>

```c
void acceleration(double x[], double y[], double dy2dx2[], int m);
```
>Parameter<br>
**x[]** : x data set <br>
**y[]** : y data set <br>
**dy2dx2[]** : 미분 값을 저장한 배열 선언 <br>
**m** : data set의 길이

1. myNP.h 안에 선언되어 있다.
2. 다음과 같은 원리를 기반으로 작성되었다.<br>

* The truncation error can be estimated using Taylor sereies.

$$f(x)=\sum_{k=0}^nf^{(k)}(x_0){{x-x_0}^k\over{k!}}+E_{n+1}$$


* Three point forward difference

$$f^{''}(x_i)={{f(x_{i})-2f(x_{i+1})+f(x_{i+2})}\over h^2}$$
$$Truncation Error:O(h)$$

* Three point backward difference

$$f^{''}(x_{i})={{f(x_{i-2})-2f(x_{i-1})+f(x_{i-2})}\over h^2}$$
$$Truncation Error:O(h)$$

* Three point central difference

$$f^{''}(x_i)={{f(x_{i-1})-2f(x_i)+f(x_{i+1})}\over h^2}$$
$$Truncation Error:O(h^2)$$

* Five point central difference
  
$$f^{''}(x_i)={{-f(x_{i-2})+16f(x_{i-1})-30f(x_i)+16f(x_{i+1})-f(x_{i+2})}\over 12h^2}$$
$$Truncation Error:O(h^4)$$

* Four point forward difference

$$f^{''}(x_{i})={{-f(x_{i+3})+4f(x_{i+2})-5f(x_{i+1})+2f(x_i)}\over h^2}$$
$$Truncation Error:O(h^2)$$

* Four point backward difference

$$f^{''}(x_{i})={{-f(x_{i-3})+4f(x_{i-1})-5f(x_{i+1})+2f(x_i)}\over h^2}$$
$$Truncation Error:O(h^2)$$
    


<hr>

## Example <br>
```c++
int main()
{
    int _m = 21;
    double t[21] = { 0 };
    for (int i = 0; i < _m; i++) t[i] = 0.2 * i;     // x = [0, 0.2, 0.4, ... 3.6, 3.8, 4]

    double y[21] = { 0 };
    double  dydt[21] = { 0 };
	for (int i = 0; i < _m; i++) {
		t[i] = i * 0.2;
		y[i] = power(t[i], 3);
	}

	acceleration(t, y, dydt, _m);
	printVec(dydt, _m);
}
```

## Output <br>
```c
Vector[0] = -0.00
Vector[1] = 1.20
Vector[2] = 2.40
Vector[3] = 3.60
Vector[4] = 4.80
Vector[5] = 6.00
Vector[6] = 7.20
Vector[7] = 8.40
Vector[8] = 9.60
Vector[9] = 10.80
Vector[10] = 12.00
Vector[11] = 13.20
Vector[12] = 14.40
Vector[13] = 15.60
Vector[14] = 16.80
Vector[15] = 18.00
Vector[16] = 19.20
Vector[17] = 20.40
Vector[18] = 21.60
Vector[19] = 22.80
Vector[20] = 24.00
```

## Warning
>The length of x and y must be equal<br>
The length of data must be more than 3

## Error Handling
```c
if (sizeof(x) != sizeof(y)) 
{
	printf("ERROR: length of x and y must be equal\n");
	return;
}


if (m < 4) 
{
	printf("ERROR: length of data must be more than 3\n");
	return;
}
```
<br>
