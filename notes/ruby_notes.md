# ruby notes
## strings
```rb
# interpolation
"#{str} "

# split to chars
s.chars

# split
puts str.split( /, */, 4 ) # get 1st**** 4
first,*rest = ex.split(/,/) # set 1st

# dequeue
s = 'abc'
s.slice(0) # 'a', s = 'bc'

# permutation
s.chars.permutation.map(&:join)

# remove non alphanum
str = str.gsub(/[^0-9a-z ]/i, '')
```

#### each
```rb
# with object
['a', 'b', 'c'].each_with_object({}).with_index do |(el, acc), index|
  acc[index] = el
end
# => {0=>"a", 1=>"b", 2=>"c"}

# with index
['a', 'b', 'c'].each_with_index do |e, i| puts i end

# offset
my_list = [1, 2, 3, 4 ,5]
my_list[3..-1].each { |i| puts i }

# frequency hash
['one', 'two', 'one', 'one'].each_with_object(Hash.new(0)) do |item, hash|
  hash[item] += 1
end
 => {"one"=>3, "two"=>1}

# pairs the start and end times then sorts by end time
  sorted = start_times.each_with_object([]).with_index do |(s, a), i|
    a << [s, end_times[i]]
  end.sort_by { |e| [e[1], e[0]] }

164

The with_index method takes an optional parameter to offset the starting index. each_with_index does the same thing, but has no optional starting index.

```

#### etc
```rb
(0..s.size-1).to_a.any?{|i|}

.compact/! # removes nils
.uniq # what you think
next if true # skips loop iteration
redo # starts from top of iteration
.include?()

if i.between?(1, 10)
if (1..10) === i

a = %w(albatross dog horse)
a.max_by { |x| x.length }   #=> "albatross"

arr = [[3,4],[5,6]]
arr.each do |a,b|
    puts "#{a} #{b}"
end

#?
arr.each_with_object({}).with_index do |(e,o), i|
    o[e] = [] if o[e].nil?
    o[e] << i
  end

max_e = freq_hash.max_by {|e| e.last.length }.last

result = case score
	when 0..59 then "Fail"
  when 60..100 then "Pass"
  else "Invalid"
```

#### for loop
```rb
for i in 0..5
  if i > 2 then
    break
  end
end

(0..5).each { |i| break if i > 2 }

last_value = [1, 2, 3].each do |n|
  break n if n % 2 == 0
end
```

#### select/filter
```rb
[1,2,3,4,5,6].select(&:even?)

fruits = %w(apple orange banana)
fruits.select.with_index { |word, idx| idx.even? }
# ["apple", "banana"]

fruits = %w(apple orange banana)
fruits.select! { |fruit| fruit.start_with? "a" }
# ["apple"]

[1,2,3,4,5,6].reject { |n| n == 4 }

# When you use select with an ActiveRecord model you're asking for specific columns from the database.

Fruit.select(:id, :name, :color)
```

#### map - the main use for map is to TRANSFORM data
```rb
hash = { bacon: "protein", apple: "fruit" }
hash.map { |k,v| [k, v.to_sym] }.to_h
# {:bacon=>:protein, :apple=>:fruit}

array = %w(a b c)
array.map.with_index { |ch, idx| [ch, idx] }
# [["a", 0], ["b", 1], ["c", 2]]

["11", "21", "5"].map(&:to_i)

h = { a: 1, b: 2, c: 3 }

# transform_values: just changing hash values
h.transform_values {|v| v * v + 1 }
# => { a: 2, b: 5, c: 10 }

h.transform_values(&:to_s)
# => { a: "1", b: "2", c: "3" }

# Map over a nested Array
my_array = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
]
my_array.map { |row| row.map { |col| col + 1 } }
# => [[2, 3, 4, 5], [6, 7, 8, 9]]

a = [1, 2, 3]
b = [4, 5, 6]
c = [7, 8, 9]

[a, b, c].transpose.map { |x| x.reduce :+ }
# => [12, 15, 18]

```

#### reduce
```rb
[1, 2, 3].reduce(0) { |sum, n| sum + n } # => 6

[1, 2, 3].sum # => 6
[1, 2, 3].min # => 1
[1, 2, 3].max # => 2
[1, 2, 3].count # => 3
[1, 2, 3, 3].count {|e| e == 3} # => 2

[1, 2, 3].reduce([]) do |m, n| 
  m << n if n == 2
  m
end

[1, 2, 3].reduce(0){|sum, indv| sum + indv} #is the same as .reduce(:+)

(1..10).reduce(:+) # same as (1..10).sum
 => 55

# very useful to find min/max of something
words.reduce do |longest, word|
  if longest.length > word.length
    longest
  else
    word
  end
end

```

#### sort
```rb
[1, 2, 3].sort { |a, b| b <=> a }  # => [3, 2, 1]

matrix.sort_by { |obj| obj.size }
# => [
  [1, 2, 3],
  [:a, :b, :c, :d],
  [1, 2, 3, 4, 5],
  [1, 2, 3, 4, 5, 6]
]

[p1, p2, p3, p4].sort_by { |p| [p.fname, p.lname] }

my_hash.sort_by { |k, v| k }

scores.sort_by { |h | h[:name] }
```

## array
```rb
[].include? val

["abc", "bcd", "dfg", "ghk"].find_index { |e| e =~ /^d.*/ } # => 2

[1, 2, 3, 4, 5, 6].sample(3) # => [2, 1, 4]

# set union
[1, 2] | [2, 3, 4] # => [1, 2, 3, 4]

Add the string "celery" to the beginning of the array:
array.unshift("celery") # add to beginning

a = %w(albatross dog horse)
a.max_by { |x| x.length }   #=> "albatross"

# stacks/queues with arrays
2.4.1 :548 > a = [1, 2, 3]
 => [1, 2, 3]

# pop/dequeue from front
2.4.1 :549 > a.shift
 => 1
2.4.1 :550 > a
 => [2, 3]

# by position
> a = [1, 2, 3]
 => [1, 2, 3]

# remove from end
> a.slice!(-1)
 => 3
> a
 => [1, 2]

# push to front
2.4.1 :551 > a.unshift(1)
 => [1, 2, 3]
2.4.1 :552 > a
 => [1, 2, 3]

# enqueue to end
2.4.1 :555 > a.push(4)
 => [0, 1, 2, 3, 4]
2.4.1 :556 > a.unshift(-1)
 => [-1, 0, 1, 2, 3, 4]


foo = Array(foo).push(:element)

[1,2].zip([3,4]) => [[1,3],[2,4]]

array.reverse

# initialize matrix/2d matrix
2.4.1 :065 > Array.new(r){Array.new(c, 0)}
 => [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
2.4.1 :066 > Array.new(r){Array.new(c, nil)}
 => [[nil, nil, nil, nil], [nil, nil, nil, nil], [nil, nil, nil, nil]]

```
---
scratch
```rb
a = [7]
b = [2]

(0..b.size).to_a.reduce { |i|
            [(a[i] - a[i-1]).abs + (b[i] - b[i-1]).abs].max
        }


n = m.map{ |e| e if e > 0 }
def array_split(n, c)
a = []
while true
  if n.index(c).nil?
    a << n
    break
  end
  a << n.slice!(0..n.index(c)-1)
  n.slice!(0) unless n.index(c).nil?
end
a
end
n.each_with_object([]) do |e, a|
	
end
```

### send
```ruby
a = [2, 2, 3]
a.send("length")
# or
a.public_send("length")

# Using call
method_object = s.method(:length) 
p method_object.call #=> 6

# Using eval
eval "s.length" #=> 6

```
