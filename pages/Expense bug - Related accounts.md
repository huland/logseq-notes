- ## Ticket details
	- [ticket](https://gitlab.vertis.com:8443/vertis/mv2/-/issues/7047)
## Notes
	- On the VertisReactSelect component the  `isMulti={false}` was sent as props, but the component behavior is not the same when this prop is `true` or `false` and the code was not updated to work without isMulti.
	- The field name is
## Review details
	- [pull request](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/459)
## Activity Summary
	- [[2023-10-11]] (30m)
		- reproduced
		- talked with #Adam.Szucs who was helping me debug and solve the issue
- tags:: #vertis #ticket