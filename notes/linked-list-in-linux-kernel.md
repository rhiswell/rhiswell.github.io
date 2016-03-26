# Linked List in Linux Kernel

## `list_head`

```c
/* linux/list.h */
struct list_head {
	struct list_head *next, *prev;
};
```

## `container_of` and `list_entry`

```c
/* linux/stddef.h */
#undef NULL
#if defined(__cplusplus)
#define NULL 0
#else
#define NULL ((void *)0)

#endif
#undef offsetof
#ifdef __compiler_offsetof
#define offsetof(TYPE,MEMBER) __compiler_offsetof(TYPE,MEMBER)
#else
#define offsetof(TYPE, MEMBER) ((size_t) &((TYPE *)0)->MEMBER)

/* linux/kernel.h */
/**
 * container_of - cast a member of a structure out to the containing structure
 * @ptr:	the pointer to the member.
 * @type:	the type of the container struct this is embedded in.
 * @member:	the name of the member within the struct.
 *
 */
#define container_of(ptr, type, member) ({			\
	const typeof( ((type *)0)->member ) *__mptr = (ptr);	\
	(type *)( (char *)__mptr - offsetof(type,member) );})

/* linux/list.h */
/**
 * list_entry - get the struct for this entry
 * @ptr:	the &struct list_head pointer.
 * @type:	the type of the struct this is embedded in.
 * @member:	the name of the list_struct within the struct.
 */
#define list_entry(ptr, type, member) \
	container_of(ptr, type, member)
```

- `offsetof(TYPE, MEMBER)`中`&((TYPE *)0)->MEMBER`为type中member在type中的偏移量（address_of(member) - address_of(type)(=0 as (type *)0) = address_of(member）。然后在`container_of`中，member的实际地址减去member在type中的偏移量，自然就是type变量的实际地址。
- 0在`(type *)0`中表示什么?见上代码段中，0即NULL，是一个无内容的指针变量。`(type *)0`即`(type *)((void *)0)`。不这样（即没有一个合法的变量），就没法访问MEMBER，更没法`typeof()`了。
- `typeof()`如何工作？`sizeof()`呢？TODO
- `offsetof`中`&((TYPE) *)0)->MEMBER`为什么需要转为`size_t`?`(char *)__mptr`为什么需要转换为`char *`？
- 为什么不能`typeof(ptr) __mptr = ptr`，而要`typeof(((type *)0)->member) *__mptr = (ptr)`?我猜，指针只是单纯保存某变量的内存地址，无法体现变量的具体类型。
- 为什么不直接`(ptr) - offsetof(type, member)`？`const typeof( ((type *)0)->member ) *__mptr = (ptr)`可以让编译器在编译时检查（ptr）的是否符合指定指针类型。

## `list_for_each` and `list_for_each_entry`

```c
/* linux/list.h */
/**
 * list_for_each	-	iterate over a list
 * @pos:	the &struct list_head to use as a loop cursor.
 * @head:	the head for your list.
 */
#define list_for_each(pos, head) \
	for (pos = (head)->next; prefetch(pos->next), pos != (head); \
        	pos = pos->next)

/**
 * list_for_each_entry	-	iterate over list of given type
 * @pos:	the type * to use as a loop cursor.
 * @head:	the head for your list.
 * @member:	the name of the list_struct within the struct.
 */
#define list_for_each_entry(pos, head, member)				\
	for (pos = list_entry((head)->next, typeof(*pos), member);	\
	     prefetch(pos->member.next), &pos->member != (head); 	\
	     pos = list_entry(pos->member.next, typeof(*pos), member))
```

- `prefetch(x)`?

## References
- [Why this 0 in ((type*)0)->member in C?](http://stackoverflow.com/questions/13723422/why-this-0-in-type0-member-in-c)