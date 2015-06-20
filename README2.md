> ## Additional examples to use with DanieleP clarifying instructions.
> ## Read the README.md file before this.
> ## Reprint functions from lecture example
> makeVector <- function(x = numeric()) {
+     m <- NULL
+     set <- function(y) {
+         x <<- y
+         m <<- NULL
+     }
+     get <- function() x
+     setmean <- function(mean) m <<- mean
+     getmean <- function() m
+     list(set = set, get = get,
+          setmean = setmean,
+          getmean = getmean)
+ }
> cachemean <- function(x, ...) {
+     m <- x$getmean()
+     if(!is.null(m)) {
+         message("getting cached data")
+         return(m)
+     }
+     data <- x$get()
+     m <- mean(data, ...)
+     x$setmean(m)
+     m
+ }
> ## Create sample vector to test functions; Verify vector and show its mean
> v <- 1:10
> v
 [1]  1  2  3  4  5  6  7  8  9 10
> mean(v)
[1] 5.5
> ##
> a <- makeVector(v)
> a
$set
function (y) 
{
    x <<- y
    m <<- NULL
}
<environment: 0x000000000b186db0>

$get
function () 
x
<environment: 0x000000000b186db0>

$setmean
function (mean) 
m <<- mean
<environment: 0x000000000b186db0>

$getmean
function () 
m
<environment: 0x000000000b186db0>

> 
> a$get
function() x
<environment: 0x000000000b186db0>
> a$get()
 [1]  1  2  3  4  5  6  7  8  9 10
> a$getmean()
NULL
> a$getmean(v)
Error in a$getmean(v) : unused argument (v)
> a$setmean(42)
> a$getmean()
[1] 42
> a <- makeVector(v)
> a$getmean()
NULL
> cachemean(a)
[1] 5.5
> a$getmean()
[1] 5.5
> a$get()
 [1]  1  2  3  4  5  6  7  8  9 10
> a <- makeVector(1:5)
> a$getmean()
NULL
> a$get()
[1] 1 2 3 4 5
> cachemean(a)
[1] 3
> cachemean(a)
getting cached data
[1] 3
> cachemean(a)
getting cached data
[1] 3
> a$setmean(45)
> a$getmean()
[1] 45
> cachemean(a)
getting cached data
[1] 45
> a$setmean(NULL)
> a$getmean()
NULL
> cachemean(a)
[1] 3
>
