# Insertion Sort

### Purpose
Sort an array

### Summary
Iterate through the array. Each time you hit an item that is lower
than the one before it, go backwards, switching the smaller item
with all the ones before it that are smaller.

### Big O
Can be twice as fast as selection sort

### Ruby

```ruby
class InsertionSort
  def sort(items)
    sorted_til_pointer = 1
    forward_pointer = 1
    backward_pointer = 0
    length = items.length

    # loop until the sorted_til_pointer reaches the end of the array
    until sorted_til_pointer == length
      current_item = items[forward_pointer]
      previous_item = items[backward_pointer]

      # until the current item is greater or equal to the one before it
      until current_item >= previous_item
        # switch what is at the current pointer with the backward pointer,
        # move the backward and forward pointers back one
        items[backward_pointer] = current_item
        items[forward_pointer] = previous_item

        if backward_pointer != 0
          backward_pointer -= 1
          forward_pointer -= 1
        end

        # update current and previous items
        current_item = items[forward_pointer]
        previous_item = items[backward_pointer]
      end

      # put the forward and backward pointers back where they started
      sorted_til_pointer += 1
      forward_pointer = sorted_til_pointer
      backward_pointer = sorted_til_pointer - 1
    end

    items
  end
end

```
