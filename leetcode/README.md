# Leetcode

### 1. Contains Duplicate (217)
[Array](),
[Hash Table]()

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

##### working solution:
time:O(n)
space:O(n)
```
def contains_duplicate(nums)
    map={}
    i = 0
    while i < nums.length
        return true if map[nums[i]] == true
        map[nums[i]]=true
        i+=1
    end
    return false
end
```

#### better solution?
sort the array first

time:O(n)
space:O(1)
```
def contains_duplicate(nums)
    nums.sort!
    i = 0
    while i < nums.size-1
        return true if nums[i]==nums[i+1]
        i+=1
    end
    return false    
end
```



### 2. Roman to Integer (13)
[Math](),
[String]()

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

#### working solution
time:O(n)
space:O(n)
```
ROMAN = {
  'I'=>1,
  'V'=>5,
  'X'=>10,
  'L'=>50,
  'C'=>100,
  'D'=>500,
  'M'=>1000
}

def roman_to_int(s)
    return 0 if s.size == 0
    num_s = s.chars.map{|char| ROMAN[char]}
    sum = 0
    i = 0

    while i < num_s.size-1
        if num_s[i+1] > num_s[i]
            sum -= num_s[i]
        else
            sum += num_s[i]
        end
        i += 1
    end
    sum + num_s[-1]
end
```


#### better solution

time:O(n)
space:O(1)
```
def roman_to_int(s)
    sum = 0
    sum -= 2 if s.index('IV')
    sum -= 2 if s.index('IX')
    sum -= 20 if s.index('XL')
    sum -= 20 if s.index('XC')
    sum -= 200 if s.index('CD')
    sum -= 200 if s.index('CM')
    s.each_char do |c|
        case c
        when 'M' then sum += 1000
        when 'D' then sum += 500
        when 'C' then sum += 100
        when 'L' then sum += 50
        when 'X' then sum += 10
        when 'V' then sum += 5
        when 'I' then sum += 1
        end
    end
    sum
end
```

### 3. Binary Watch(401)
[Math](),
[String]()

A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59).

Each LED represents a zero or one, with the least significant bit on the right.

Given a non-negative integer n which represents the number of LEDs that are currently on, return all possible times the watch could represent.

Example:
```
Input: n = 1
Return: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
```

#### working solution
