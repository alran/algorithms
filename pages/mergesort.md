# Mergesort

### Purpose
Sort an array of items.

### Summary
Divide the array in half, recursively sort each half, merge the two halves. Cons: 
too much overhead for small arrays

### Big O
N log N

### Ruby

```ruby
class MergeSort
  def sort(elements)
    length = elements.length

    # split the array in half
    halves = elements.each_slice((length/2.0).ceil).to_a

    # sort the two arrays
    sorted_halves = halves.map(&:sort)

    # instantiate a final array
    final = []

    # instantiate current pointers for all arrays (halves + final)
    i = 0
    j = 0
    k = 0

    until final.length == length
      current1 = sorted_halves[0][i]
      current2 = sorted_halves[1][j]

      if current1 && (current2.nil? || current1 < current2)
        final << current1
        i += 1
      else
        final << current2
        j += 1
      end

      k += 1
    end

    final
  end
end

```
