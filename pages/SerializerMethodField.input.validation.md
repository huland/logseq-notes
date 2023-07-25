- [PR comment](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/312#note_13229) #Adam.Szucs tried to resolve my PR comment but when he created a method for validation:
- ```python
  def validate_ets_offers(self, value):
  	...
      
  ```
- the validation does not run, the ets_offer is a `serializers.SerializerMethodField()`