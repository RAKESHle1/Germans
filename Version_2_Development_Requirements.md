# Version 2 Development Requirements

The **Version1_fixed** notebook is now considered the primary and finalized implementation. Based on the feedback received, it appears to satisfy the assignment requirements successfully. Therefore, our focus should now shift entirely to developing **Version 2**.

For **Version 2**, we should maintain the same assignment objectives and satisfy all the required evaluation criteria, but the implementation must be sufficiently different from Version 1 so that both notebooks appear to have been developed independently.

## Machine Learning Model

In Version 1, we used the **Random Forest** algorithm for the machine learning forecasting section. To further differentiate Version 2 and minimize implementation similarity, we should replace Random Forest with the **Gradient Boosting** algorithm (or an equivalent gradient boosting implementation that is appropriate for the assignment).

This change should not compromise the assignment requirements or forecasting performance. The selected model should be properly justified, evaluated, and compared with the benchmark forecasting models.

## Version 2 Development Guidelines

While developing Version 2, keep all of the previously identified observations and issues in mind, including:

- The SARIMA model selection and justification.
- Seasonal parameter selection and validation.
- Proper model selection based on statistical evidence.
- Clear technical justifications for every important design decision.
- Verification of the LSTM evaluation and alignment.
- Complete compliance with every assignment requirement.

Any improvements or corrections incorporated into Version 1 should also be reflected appropriately in Version 2 whenever applicable.

## Code Independence Requirements

Version 2 should be implemented as if it were developed by a completely different student. Although both notebooks solve the same problem and follow the same assignment requirements, the implementation style should be significantly different.

The following components should be redesigned:

- Use completely different variable names.
- Use different function names.
- Rename helper functions.
- Change intermediate variables.
- Reorganize the notebook structure where appropriate.
- Rewrite all markdown explanations.
- Rewrite all code comments.
- Modify the execution flow where possible while preserving correctness.
- Use different visualization styles, including:
  - Different color palettes
  - Different chart styles where appropriate
  - Different figure layouts
  - Different marker and line styles
  - Different titles and axis labels
  - Different annotation styles

The notebook should present the same analytical workflow while exhibiting a distinctly different coding style and presentation.

## Originality and Academic Integrity

One of the highest priorities for Version 2 is maintaining clear implementation independence from Version 1.

The objective is to ensure that:

- The implementation structure is substantially different.
- The coding style is different.
- Variable naming conventions are different.
- Function implementations are different wherever possible.
- Visualizations are noticeably different.
- Documentation and markdown explanations are independently written.

Although the underlying machine learning concepts and assignment logic will naturally remain the same, the overall implementation should appear to have been created independently.

The target is to minimize implementation similarity to approximately **1–2%**, while ensuring that both notebooks fully satisfy the assignment requirements and maintain the same level of technical quality.

## Final Expectation

Before finalizing Version 2, perform a comprehensive review of the entire notebook to ensure:

- All assignment requirements are satisfied.
- All previously identified issues have been addressed.
- The notebook executes successfully from beginning to end.
- All models are statistically justified.
- All visualizations are correct.
- All evaluation metrics are accurate.
- The implementation is technically sound, reproducible, and professionally documented.

The final Version 2 notebook should be a high-quality, independent implementation that meets the same academic standards as Version 1 while maintaining a clearly distinct implementation style.
