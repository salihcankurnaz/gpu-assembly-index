# Model Provenance

## `ma_model.pt`

`ma_model.pt` is a PyTorch `state_dict` artifact produced by the training workflow in
`nn_predictor.py`.

The current training script:

1. generates molecule strings programmatically in `generate_molecules()`;
2. computes target MA values with the repository's `compute_ma()` implementation;
3. converts molecules to Morgan fingerprints with RDKit;
4. trains the `MAPredictor` neural network; and
5. writes the best model weights with `torch.save(model.state_dict(), model_path)`.

This training path does not require an external downloaded training dataset. RDKit,
PyTorch, NumPy, and other dependencies remain subject to their own licenses.

The artifact is distributed as part of this project under the repository's MIT License.
This is a technical provenance statement, not a legal conclusion about the copyright or
database-law status of generated model weights in every jurisdiction.
