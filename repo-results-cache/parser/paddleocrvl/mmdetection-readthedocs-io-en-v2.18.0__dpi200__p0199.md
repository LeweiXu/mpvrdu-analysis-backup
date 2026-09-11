## Type None | LongTensor

## Example

>>> # An assign result between 4 predicted boxes and 9 true boxes
>>> # where only two boxes were assigned.
>>> num_gts = 9
>>> max_overlaps = torch.LongTensor([0,.5,.9, 0])
>>> gt_inds = torch.LongTensor([-1, 1, 2, 0])
>>> labels = torch.LongTensor([0, 3, 4, 0])
>>> self = AssignResult(num_gts, gt_inds, max_overlaps, labels)
>>> print(str(self))  # xdoctest: +IGNORE_WANT
<AssignResult(num_gts=9, gt_inds.shape=(4,), max_overlaps.shape=(4,), labels.shape=(4,))>
>>> # Force addition of gt labels (when adding gt as proposals)
>>> new_labels = torch.LongTensor([3, 4, 5])
>>> self.add_gt_ (new_labels)
>>> print(str(self))  # xdoctest: +IGNORE_WANT
<AssignResult(num_gts=9, gt_inds.shape=(7,), max_overlaps.shape=(7,), labels.shape=(7,))>

## add_gt_(gt_labels)

Add ground truth as assigned results.

Parameters gt_labels (torch.Tensor) – Labels of gt boxes

## get_extra_property(key)

Get user-defined property.

## property info

Type dict

## property num_preds

Type int

## classmethod random(**kwargs)

Create random AssignResult for tests or debugging.

## Parameters

• num_preds – number of predicted boxes

• num_gts – number of true boxes

• p_ignore (float) – probability of a predicted box assigned to an ignored truth

• p_assigned (float) – probability of a predicted box not being assigned

• p_use_label (float / bool) – with labels or not

• rng (None / int / numpy.random.RandomState) – seed or state

Returns Randomly generated assign results.

Return type AssignResult