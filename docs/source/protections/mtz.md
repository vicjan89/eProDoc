# Максимальная токовая защита (МТЗ)

Для расчёта уставок необходимо заполнить поля:
    Наименование
    Максимальный рабочий ток, А
    Примечание для максимального рабочего тока
    Коэффициент отстройки
    Коэффициент возврата
    Коэффициент самозапуска
    Номинальная мощность, кВА (для расчёта базисного тока)
    vn_kv = models.FloatField(blank=True, null=True, verbose_name='Номинальное линейное напряжение системы, кВ')
    x_system = models.FloatField(blank=True, null=True, verbose_name='Сопротивление системы, Ом')
    x_motors = models.FloatField(blank=True, null=True,
                                 verbose_name='Сопротивление заторможенных двигателей нагрузки, Ом')
    i_kz_min = models.FloatField(blank=True, null=True, verbose_name='Ток КЗ в основной зоне, минимальный, А')
    i_kz_end_index = models.PositiveIntegerField(blank=True, null=True,
                                                 verbose_name='Индекс узла в конце основной зоны защиты')
    kt = models.FloatField(blank=True, default=1., verbose_name='Кт узла конца основной зоны')
    i_kz_min_note = models.CharField(max_length=100, blank=True, default='',
                                     verbose_name='Примечание к току КЗ в основной зоне минимальному')
    i_kz_min_res = models.FloatField(blank=True, null=True, verbose_name='Ток КЗ в зоне резервирования, минимальный, А')
    index_kz_min_res = models.PositiveIntegerField(blank=True, null=True,
                                                   verbose_name='Индекс узла в конце зоны резервирования')
    kt_res = models.FloatField(blank=True, default=1., verbose_name='Кт узла конца резервной зоны')
    i_kz_min_res_note = models.CharField(max_length=100, blank=True, null=True,
                                         verbose_name='Примечание к току КЗ в зоне резервирования минимальному')
    isz_posl = models.FloatField(blank=True, null=True, verbose_name='Ток срабатывания последующей МТЗ, А')
    isz_posl_note = models.CharField(max_length=100, blank=True, null=True,
                                     verbose_name='Примечание к току срабатывания последующей МТЗ')
    isz_prev = models.FloatField(blank=True, null=True, verbose_name='Ток срабатывания предыдущей МТЗ, А')
    isz_prev_note = models.CharField(max_length=100, blank=True, null=True,
                                     verbose_name='Примечание к току срабатывания предыдущей МТЗ')
    kns = models.FloatField(blank=True, default=1.1, verbose_name='Коэффициент согласования')
    isz = models.FloatField(blank=True, null=True, verbose_name='Ток срабатывания, А')
    isz_note = models.CharField(max_length=100, blank=True, null=True, verbose_name='Примечание к току срабатывания')

    v = models.FloatField(blank=True, null=True, verbose_name='Напряжение пуска, В')
    vn_min_v = models.FloatField(blank=True, null=True,
                                 verbose_name='Напряжение номинальное в месте подключения органа минимального напряжения, В')
    kv_vmin = models.FloatField(blank=True, default=1.04,
                                verbose_name='Коэффициент возврата органа минимального напряжения')
    direction_choises = {'': '',
                        'от шин в линию': 'от шин в линию',
                        'от линии к шинам': 'от линии к шинам',
                        'ненаправленная': 'ненаправленная'}
    direction = models.CharField(verbose_name='Направление', blank=True,
                                 default='', max_length=30,
                                 choices=direction_choises)

    t = models.FloatField(blank=True, null=True, verbose_name='Время срабатывания, сек.')
    t_note = models.CharField(max_length=100, blank=True, null=True, verbose_name='Примечание ко времени',
                              help_text='Куда действует по истечении времени или порядок выбора')
    k = models.FloatField(blank=True, null=True, verbose_name='Коэффициент, характеризующий вид зависимой характеристики')
    t_au = models.FloatField(blank=True, null=True, default=0.5, verbose_name='Время АУ, сек.',
                             help_text='автоматического ускорения')
    bl = models.BooleanField(blank=True, null=True, verbose_name='Блокирует ли ЛЗШ при пуске')
    exclude = models.BooleanField(default=False, verbose_name='Исключить из выбора уставок', blank=True)
    ctw = models.ForeignKey(to='LoadCT', blank=True, null=True, on_delete=models.SET_NULL,
                            verbose_name='Обмотка трансформатора тока')
    vtw = models.ForeignKey(to='LoadVT', blank=True, null=True, on_delete=models.SET_NULL,
                            verbose_name='Обмотка трансформатора напряжения')
    parent = models.ForeignKey('Pris', on_delete=models.CASCADE, null=True, blank=True, related_name='mtz',
                            verbose_name='Присоединение')
