- [PR comment](https://gitlab.vertis.com:8443/vertis/mv2/-/merge_requests/312#note_13229) @AdamSzucs tried to resolve my PR comment but when he created a method for validation:
- ```python
  def validate_ets_offers(self, value):
  	...
      
  ```
- This validation does not run with this implementation, the ets_offer is a `serializers.SerializerMethodField()`