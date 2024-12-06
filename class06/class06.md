# class06


MY first function :-)

``` r
ADD <- function(x, y=1) {
  x+y
}
```

Can I just use it?

``` r
ADD(13, 17)
```

    [1] 30

``` r
ADD(x=1, y=100)
```

    [1] 101

``` r
ADD(c(100, 1, 100), 1)
```

    [1] 101   2 101

``` r
ADD(10)
```

    [1] 11

# A second function

Let’s try something more interesting

``` r
#generate_DNA <- function() {
bases <- c("A", "T", "C", "G")
sequence <- sample(bases, size=10, replace=TRUE, prob=NULL)
```

That is my wee working snippet, now, I can make it into a function.

``` r
generate_DNA <- function(length){
  bases <- c("A", "T", "C", "G")
  sequence <- sample(bases, size=length,
                     replace=TRUE)
  return(sequence)
}
```

``` r
generate_DNA(length=10)
```

     [1] "T" "T" "A" "C" "A" "A" "T" "T" "T" "G"

``` r
aa <- unique(bio3d::aa.table$aa1)[1:20]
sequence <- sample(aa, size=10, replace=TRUE, prob=NULL)
```

Theres diff chemistry of repeat amino acids

Generate a protein sequence with 10 amino acids.

``` r
generate_prot <- function(length){
  aa <- unique(bio3d::aa.table$aa1)[1:20]
  sequence <-sample(aa, size=length, replace=TRUE, prob=NULL)
sequence <- paste(sequence, collapse = "") #make the string a phrase without any spaces, concatenate multiple strings
  return(sequence)

}
```

Generate random protein sequences of length 6 to 12

``` r
answer <- sapply(6:12, generate_prot)
answer
```

    [1] "GSNYAH"       "SMCHQLN"      "GYGEVMHG"     "CEQLIAEIT"    "WHHPHHIKSP"  
    [6] "PWQVVSDSTIS"  "IFSPKEMHAHGP"

``` r
paste(c("barry", "alice", "amy", "chandra"), "loves R",sep="")
```

    [1] "barryloves R"   "aliceloves R"   "amyloves R"     "chandraloves R"

``` r
cat(paste(">id.", 6:12, "\n", answer, sep=""), sep="\n")
```

    >id.6
    GSNYAH
    >id.7
    SMCHQLN
    >id.8
    GYGEVMHG
    >id.9
    CEQLIAEIT
    >id.10
    WHHPHHIKSP
    >id.11
    PWQVVSDSTIS
    >id.12
    IFSPKEMHAHGP
