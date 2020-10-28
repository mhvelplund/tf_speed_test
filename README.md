# for_each considered harmful

Based on internet rumors I wrote some sample templates and timed their planning.
All the examples create a 1000 buckets. 

## Test
Running the tests on devops2 with 2 CPU cores:

* [loop](./loop/main.tf): use `for_each` loop:
```
real    0m13.573s
user    0m42.134s
sys     0m0.623s
```
* [loop_output](./loop_output/main.tf): use `for_each` loop, output the ids:
```
real    5m26.874s
user    8m28.932s
sys     0m9.135s
```
* [unrolled](./unrolled/main.tf): use repeated resources:
```
real    0m9.126s
user    0m20.574s
sys     0m1.143s
```
* [unrolled_output](./unrolled_output/main.tf): use repeated resources, output the ids:
```
real    0m10.379s
user    0m23.350s
sys     0m1.454s
```

## Conclusion
Referencing elements created directly, rather than those created by a loop, is almost 30 times faster.