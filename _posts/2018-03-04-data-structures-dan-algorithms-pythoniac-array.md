---
layout: post
title: "Data Structures dan Algorithms Pythoniac - Array Vol.1"
categories:
  - Python
tags:
  - python
  - data structures
  - array
  - algorithm
---

Contoh Implementasi dari `data structure` dan `algorithm` pada Array Python

 ##  1. circular_counter
	 
Ada  beberapa orang yang duduk dalam mode melingkar, `print` setiap anggota ketiga ketika kita menghilangkannya, perhitungan berikutnya akan dimulai setelah anggota tersebut dihilangkan. `print` sampai semua anggota orang tersebut habis. Gunakan `parameter` nomor urut dalam `list` dan `variable` angka kelipatan untuk menghilangkan anggota tersebut.

**Contoh:**
	
 - *Input*: Misalkan ada sembilan orang duduk melingkar dengan nomor urut
   123456789 
   
 - *Output*: 369485271
 
 **Code:**

    a = \['1','2','3','4','5','6','7','8','9'\]

    def circular_counter(int_list, skip):
      skip = skip - 1 #list mulai dari index 0
      idx = 0
      len_list = (len(int_list))
      while len_list>0:
        idx = (skip+idx)%len_list 
        print(int_list.pop(idx))
        len_list -= 1
		
		circular_counter(a,3)

##  2. flatten
Implementasi dari `Flatten Arrays`
Misalkan diketahui `array` yang mengandung `nested arrays`, hilangkan `nested arrays` tersebut menjadi `single array`.

**Contoh:**
	
 - *Input*: a = \[2, 1, \[3, \[4, 5\], 6\], 7, \[8\]\]; 
   
 - *Output*: a = \[2, 1, 3, 4, 5, 6, 7, 8\]

 **Code:**

    import collections
    
    def flatten(inputArr, outputArr=None):
	    if not outputArr:
		    outputArr = []
	    for ele in inputArr:
		    if isinstance(ele, collections.Iterable):
			    flatten(ele, outputArr)
			else:
				outputArr.append(ele)
		return outputArr

 ## 3. garage
 Ada sebuah tempat parkir yang hanya ada satu spot kosong. Susunan tempat parkir dituliskan dalam bentuk array, dimana 0 sebagai spot kosong dan bilangan lainnya yang berbeda merepresentasikan mobil yang berbeda. Diberikan dua array sebagai `initial state` dan `final state`. Setiap `step` kita hanya boleh menggeser satu mobil dari posisinya semula dan menggesernya ke spot yang kosong. Tujuannya adalah menemukan step terkecil untuk mengubah `initial state` menjadi `final state`.

**Contoh:**
	
 - *Input*: initial = \[1,2,3,0,4\] 
 - *Output*: final = \[0,3,2,1,4\]
- Note: Kita bisa menukarkan 1 dengan 0 untuk mendapatkan [0,2,3,1,4] dst. Setiap step hanya boleh menukarkannya dengan 0

 **Code:**
 
	    def garage(initial, final):
	        steps = 0
	        while initial != final:
		        zero = initial.index(0)
		        if zero != final.index(0):
			        car_to_move = final[zero]
			        pos = initial.index(car_to_move)
			        initial[zero], initial[pos] = initial[pos], initial[zero]
	        else:
				    for i in range(len(initial)):
					    if initial[i] != final[i]:
						    initial[zero], initial[i] = initial[i], initial[zero]
					    break
			  steps += 1
	    return steps

 ## 4. longest_non_repeat
Diketahui sebuah `string`, temukan `length` dari `substring` terpanjang tanpa mengulangi karakter yang sudah ada.

**Contoh:**
	
 - `String` "abcabcbb", outputnya adalah "abc" dengan `length` sebanyak 3
 - `String` "bbbb", outputnya adalah "b" dengan `length` sebanyak 1
-  `String` "pwwkew", outputnya adalah "wke" dengan `length` sebanyak 3
- Note: Perhatikan bahwa hasilnya adalah substring, "pwke" bisa saja menjadi output tapi itu bukan `substring`

**Code:**
		
		def longest_non_repeat(string):
		    if string is None:
			    return 0
		    temp = []
		    max_len = 0
		    
		    for i in string:
			    if i in temp:
				    temp = []
			    temp.append(i)
			    max_len = max(max_len, len(temp))
		    return max_len
    
    	def longest_non_repeat_two(string):
		    if string is None:
				return 0
		    start, max_len = 0, 0
		    used_char = {}
		    for index, char in enumerate(string):
				if char in used_char and start <= used_char[char]:
				    start = used_char[char] + 1
				 else:
				    max_len = max(max_len, index - start + 1)
				    used_char[char] = index
		    return max_len
		
		string = "abcabcdefbb"
		print(string)
		print(longest_non_repeat(string))
		print(longest_non_repeat_two(string))

## 5. merge_intervals
Diketahui sebuah `collection` dari interval-interval, `merge` semua interval yang `overlap` satu dengan yang lain.

**Contoh:**
- *Input*: [1, 3], [2, 6], [8, 10], [15, 18]
- *Output*: [1, 6], [8, 10], [15, 18]

**Code:**

  ```python
	class Interval(object):
      def __init__(self, s=0, e=0):
			    self.start = s
			    self.end = e

  def merge(intervals):
		  """
		  :type intervals: List[Interval]
		  :rtype: List[Interval]
		  """
		  out = []
		  for i in sorted(intervals, key=lambda i: i.start):
			    if out and i.start <= out[-1].end:
				      out[-1].end = max(out[-1].end, i.end)
			    else:
				      out += i,
		  return out

	def print_intervals(intervals):
      res = []
		  for i in intervals:
			    res.append('['+str(i.start)+','+str(i.end)+']')
		  print("".join(res))

  def merge_intervals(l):
		  #sort
		  if l is None:
			    return None
		  l.sort(key=lambda i: i[0])
		  out = [l.pop(0)]
		  for i in l:
			    if out[-1][-1] >= i[0]:
				      out[-1][-1] = max(out[-1][-1], i[-1])
			    else:
				      out.append(i)
		  return out

  if __name__ == "__main__":
      given = [[1, 3],[2, 6],[8, 10],[15, 18]]
      intervals = []
      for l, r in given:
        intervals.append(Interval(l,r))
      print_intervals(intervals)
      print_intervals(merge(intervals))
      print(merge_intervals[given])
  ```
  
## 6. missing_ranges
 
Temukan `missing ranges` diantara `low` dan `high` dalam sebuah array

**Contoh:**
 - *Input*: array = [3, 5], low = 1, hi = 10 
 - *Output*: [1->2, 4, 6->10]

**Code:**

  ```python
  def missing_ranges(nums, lo, hi):
      res = []
      start = lo
      for num in nums:
          if num < start:
              continue
          if num == start:
              start += 1
              continue
          res.append(get_range(start, num-1))
          start = num + 1
      if start <= hi:
          res.append(get_range(start, hi))
      return res

  def get_range(n1, n2):
      if n1 == n2:
          return str(n1)
      else:
          return str(n1) + "->" + str(n2)

  nums = [3, 5, 10, 11, 12, 15, 19]
  print("original:", nums)
  print("missing range: ", missing_ranges(nums,0,20))
  ```
