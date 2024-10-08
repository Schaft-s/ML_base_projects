### 1. **Batch Normalization и Dropout на инференсе**

**Batch Normalization (BN):**
- **Во время тренировки:** Batch normalization нормализует каждый мини-батч данных, вычитая среднее значение и деля на стандартное отклонение, вычисленные внутри этого батча. После этого к нормализованным значениям применяется линейное преобразование с обучаемыми параметрами (смещение и масштабирование).
- **На инференсе:** На этапе инференса (предсказаний) нормализация выполняется с использованием глобальных статистик (среднего значения и дисперсии), которые были накоплены в процессе тренировки. Это позволяет избежать зависимости от конкретного мини-батча и использовать стабильные значения для предсказаний.

**Dropout:**
- **Во время тренировки:** Dropout выключает случайные нейроны (устанавливает их значения в ноль) с определённой вероятностью, что помогает избежать переобучения и делает модель более устойчивой.
- **На инференсе:** На инференсе Dropout отключается, и модель использует все нейроны. При этом весовые коэффициенты, связанные с отключенными нейронами, масштабируются, чтобы компенсировать эффект дропаута во время тренировки. Это приводит к тому, что на этапе предсказания модель работает полным объёмом, что делает её более стабильной и предсказуемой.

### 2. **Кросс-энтропия и её применение**

**Кросс-энтропия** — это функция потерь, которая измеряет разницу между двумя распределениями вероятностей: предсказанным моделью распределением и истинным распределением меток классов.

Формально, кросс-энтропия для задачи классификации с \(C\) классами определяется как:

\[
L = -\sum_{i=1}^{C} y_i \log(p_i)
\]

где:
- \(y_i\) — истинная метка класса (1 для правильного класса и 0 для остальных),
- \(p_i\) — вероятность, предсказанная моделью для класса \(i\).

**Применение:**
- **Бинарная классификация:** В задачах бинарной классификации используется бинарная кросс-энтропия.
- **Многоклассовая классификация:** В задачах, где классов несколько, применяется многоклассовая кросс-энтропия, часто в связке с функцией softmax.
- **Многозначная классификация:** Используется, когда модель должна предсказать вероятность принадлежности к нескольким классам одновременно (например, распознавание нескольких объектов на изображении).

Кросс-энтропия широко используется как функция потерь в задачах классификации, поскольку она напрямую измеряет разницу между истинными метками и предсказаниями модели, и её минимизация приводит к улучшению точности модели.

### 3. **Смысл теоремы Байеса для машинного обучения**

**Теорема Байеса** является основой для ряда алгоритмов машинного обучения, особенно в вероятностных моделях. Она определяет способ обновления вероятности гипотезы на основе новой информации.

Формула Байеса:

\[
P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}
\]

где:
- \(P(A|B)\) — апостериорная вероятность гипотезы \(A\) после наблюдения данных \(B\),
- \(P(B|A)\) — вероятность наблюдать данные \(B\) при условии, что гипотеза \(A\) верна,
- \(P(A)\) — априорная вероятность гипотезы \(A\),
- \(P(B)\) — маргинальная вероятность наблюдения данных \(B\).

**Значение для машинного обучения:**
- **Наивный байесовский классификатор:** Один из простейших и эффективных методов, использующих теорему Байеса. Он предполагает независимость признаков и используется в задачах классификации.
- **Апостериорная вероятность:** Теорема Байеса позволяет обновлять знания (вероятности) о гипотезах по мере поступления новой информации, что полезно в моделях, где важно учитывать новые данные.
- **Интерпретация данных:** Она помогает моделям рассматривать данные с вероятностной точки зрения, что важно для понимания и предсказания реальных процессов.

### 4. **Dice Loss**

**Dice Loss** — это функция потерь, используемая в задачах сегментации изображений. Она основана на коэффициенте Dice, который измеряет сходство между двумя множествами, например, предсказанными и истинными областями сегментации.

Формула Dice Loss:

\[
\text{Dice Loss} = 1 - \frac{2 |A \cap B|}{|A| + |B|}
\]

где:
- \(A\) — предсказанная область,
- \(B\) — истинная область.

**Интерпретация:**
- Dice Loss минимизируется, когда предсказанные области максимально совпадают с истинными областями.
- Он особенно эффективен в задачах сегментации, где может быть значительный дисбаланс классов (например, маленький объект на большом фоне), так как больше фокусируется на перекрытии между предсказаниями и истиной.

**Применение:**
- **Медицинская сегментация:** Широко используется в медицине для сегментации изображений, таких как МРТ, где важно точно выделять маленькие структуры.
- **Задачи с дисбалансом классов:** Подходит для задач, где один класс значительно больше другого, так как традиционные функции потерь, такие как кросс-энтропия, могут игнорировать малые объекты.
