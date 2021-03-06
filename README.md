# cal: Go (golang) calendar library for dealing with holidays and work days

This library augments the Go time package to provide easy handling of holidays
and work days (business days).

Holiday instances can be exact days, floating days such as the 3rd Monday of
the month, yearly offsets such as the 100th day of the year, or the result of
custom function executions for complex rules.

The Calendar type provides functions for calculating workdays and dealing 
with holidays that are observed on alternate days when they fall on weekends.

Here is a simple usage example of a cron job that runs once per day:
```go
package main

import (
	"time"

	"github.com/rickar/cal"
)

func main() {
	c := cal.NewCalendar()

	// add holidays for the business
	c.AddHoliday(cal.US_Independence)
	c.AddHoliday(cal.US_Thanksgiving)
	c.AddHoliday(cal.US_Christmas)

	t := time.Now()

	// run different batch processing jobs based on the day

	if c.IsWorkday(t) {
		// create daily activity reports
	}

	if cal.IsWeekend(t) {
		// validate employee time submissions
	}

	if c.WorkdaysRemain(t) == 10 {
		// 10 business days before the end of month
		// send account statements to customers
	}

	if c.WorkdaysRemain(t) == 0 {
		// last business day of the month
		// execute auto billing transfers
	}
}
```
