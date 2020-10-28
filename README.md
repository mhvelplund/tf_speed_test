# for_each considered harmful

Based on internet rumors I wrote some sample templates and timed their planning.
All the examples create a 1000 buckets. 

## Test
Running the tests on devops2 with 4 CPU, 16 gig RAM cores with Terraform 0.12.29:

* [loop](./loop/main.tf): use `for_each` loop:
```
real    0m13.573s
user    0m42.134s
sys     0m0.623s
```
* [loop_count](./loop_count/main.tf): use `count` loop:
```
real    0m7.059s
user    0m16.211s
sys     0m0.655s
```
* [loop_output](./loop_output/main.tf): use `for_each` loop, output the ids:
```
real    5m26.874s
user    8m28.932s
sys     0m9.135s
```
* [loop_count_output](./loop_count_output/main.tf): use `count` loop, output the ids:
```
real    7m9.471s
user    14m9.690s
sys     0m15.683s
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

* **Referencing elements created directly, rather than those created by a for_each loop, is almost 30 times faster.**
* **Referencing elements created directly, rather than those created by a count loop, is almost 40 times faster.**
* Creating elements with for_each loops is slightly slower than creating them directly.
* Creating elements with count loops is slightly faster than creating them directly.
